# Unidad 3

## Bitácora de proceso de aprendizaje

#### Acividad 1 

#### Enunciado

Luego ver el video con la charla de Robert Hodgin, te dejo la bitácora para que desahogues tus pensamientos, emociones, reflexiones, preguntas, etc, sobre lo que viste y escuchaste. Te dejo una pista de lo que yo estoy sintiendo ahora: estamos, cada vez más, dejando de usar “partes del cerebro”. Nos rendimos ante la inmediatez del resultado. El esfuerzo, el proceso, el asombro, la exploración, el descubrimiento, la frustración, todos, se diluyen. Comemos sin masticar. Vivmos en un sistema económico insaciable. Ya no importa aprender, importa ganar, aunque uno no sepa qué. Nos convertimos, ojalá, lentamente en diletantes que no tienen más alternativa que consumir lo que el algoritmo tenga para ofrecer. Y aún estoy preguntándome si así vale la pena…


#### Solución 

Pienso que revisandolo de una forma objetiva podemos ver a la IA como una herramienta que se volvio fundamental para todo tipo de trabajos, pero es cierto lo que habla el expositor, de una u otra forma no deberiamos de dejar que la IA haga todo el trabajo ya que no habria ese toque humano que hacen que las obras sean unicas 

#### Acividad 2

#### Enunciado

Reporta en tu bitácora tus reflexiones sobre lo que acabas de aprender.

#### Solución 

En esta actividad me di cuenta de que programar movimiento es literalmente imitar la vida real. Me pareció muy curioso el detalle de tener que multiplicar la aceleración por cero al final de cada frame. Al principio no le veía el sentido, pero luego lo entendí: la aceleración es como dar un empujón. Si no "reseteas" ese empujón constantemente, el objeto acumularía la fuerza y saldría volando sin control, como si le dejaras el acelerador metido a fondo a una moto sin soltarlo nunca.

#### Acividad 3

#### Enunciado

En tu bitácora, vas a crear tres obras generativas para cada una de las siguientes fuerzas:

Fricción.
Resistencia al aire y fluidos
Atracción gravitacional.

#### Solución 

## 1. Ejercicio Fricción 

```c
let mover;

function setup() {
  createCanvas(600, 400);
  mover = new Mover(50, height / 2, 3);
  
  // Le damos un fuerte empujón inicial simulando aceleración
  let initialImpulse = createVector(20, 0);
  mover.applyForce(initialImpulse);
}

function draw() {
  background(240);

  // 1. Calcular la fricción
  let friction = mover.velocity.copy();
  friction.normalize();
  friction.mult(-1); // Dirección opuesta a la velocidad
  
  let mu = 0.05; // Coeficiente de fricción (ej. llanta vs asfalto)
  let normal = 1; // Fuerza normal simplificada
  friction.setMag(mu * normal);

  // 2. Aplicar la fricción solo si el objeto se está moviendo
  if (mover.velocity.mag() > 0.1) {
    mover.applyForce(friction);
  } else {
    // Detener por completo para evitar micro-movimientos extraños
    mover.velocity.mult(0); 
  }

  mover.update();
  mover.checkEdges();
  mover.show();
  
  // Dibujar el "suelo"
  fill(50);
  noStroke();
  rect(0, height/2 + 24, width, height);
}
```
<img width="746" height="495" alt="image" src="https://github.com/user-attachments/assets/d1d6635e-923f-47c8-bcb2-e90a2da8842b" />


## 2. Ejercicio Resistencia al aire y fluidos 
```c
let movers = [];

function setup() {
  createCanvas(600, 400);
  // Creamos varios objetos con diferentes masas
  for (let i = 0; i < 5; i++) {
    movers[i] = new Mover(random(50, width-50), 0, random(1, 4));
  }
}

function draw() {
  background(255);

  // Dibujar el "líquido" en la mitad inferior
  noStroke();
  fill(0, 150, 255, 100);
  rect(0, height / 2, width, height / 2);

  for (let mover of movers) {
    // Fuerza 1: Gravedad (escalada por la masa para que caigan igual)
    let gravity = createVector(0, 0.1 * mover.mass);
    mover.applyForce(gravity);

    // Si el objeto cruza la mitad de la pantalla, entra al "fluido"
    if (mover.position.y > height / 10) {
      // 1. Invertir dirección de la velocidad
      let drag = mover.velocity.copy();
      drag.normalize();
      drag.mult(-1);

      // 2. Calcular c * v^2
      let c = 0.05; // Coeficiente de arrastre del fluido
      let speedSq = mover.velocity.magSq();
      drag.setMag(c * speedSq);

      // 3. Aplicar fuerza de arrastre
      mover.applyForce(drag);
    }

    mover.update();
    mover.checkEdges();
    mover.show();
  }
}
```
<img width="751" height="496" alt="image" src="https://github.com/user-attachments/assets/f3ef3e16-8e00-40b0-adc1-098abb2cc15e" />

## 3. Atracción gravitacional.
```c
let movers = [];
let attractor;

function setup() {
  createCanvas(600, 600);
  for (let i = 0; i < 10; i++) {
    movers[i] = new Mover(random(width), random(height), random(0.5, 2));
    // Damos una velocidad inicial perpendicular para crear órbitas
    movers[i].velocity = p5.Vector.random2D().mult(random(2, 5));
  }
  attractor = new Attractor(width / 2, height / 2, 20);
}

function draw() {
  // Un fondo con baja opacidad deja una "estela" del movimiento
  background(20, 20, 30, 50);

  attractor.show();

  for (let mover of movers) {
    // El atractor calcula la fuerza de gravedad y se la aplica al mover
    let force = attractor.calculateAttraction(mover);
    mover.applyForce(force);

    mover.update();
    mover.show();
  }
}

// --- CLASE ATTRACTOR (Exclusiva de este sketch) ---
class Attractor {
  constructor(x, y, m) {
    this.position = createVector(x, y);
    this.mass = m;
    this.G = 1.2; // Constante gravitacional
  }

  calculateAttraction(mover) {
    let force = p5.Vector.sub(this.position, mover.position);
    let distance = force.mag();
    // Restringimos la distancia para que no salgan disparados al infinito si se acercan mucho
    distance = constrain(distance, 5, 25); 
    force.normalize();

    let strength = (this.G * this.mass * mover.mass) / (distance * distance);
    force.mult(strength);
    
    return force;
  }

  show() {
    noStroke();
    fill(255, 100, 100);
    circle(this.position.x, this.position.y, this.mass * 2);
  }
}
```

<img width="738" height="690" alt="image" src="https://github.com/user-attachments/assets/e505d8b8-f7c5-4050-a801-cd747d920393" />


## Bitácora de aplicación 

#### Acividad 4

#### Enunciado

Describe el concepto de tu obra generativa. Explica la historia que quieres contar y cómo crees que esta influencierá las fuerzas que usarás para manipular la aceleración de los elementos visuales. Es decir, explica cómo las fuerzas moldearán las reglas que determinarán las fuerzas.
El código de la aplicación.
Un enlace al proyecto en el editor de p5.js.
Selecciona capturas de pantalla representativas de tu pieza de arte generativa.

#### Solución 

#### Historia 

Mi obra generativa esta inspirada en la mitología nórdica y el universo visual de God of War. La pieza representa a Yggdrasil, el Árbol del Mundo, que actúa como el nucleo vital del cosmos, su alrededor fluyen constantemente las runas antiguas, que representan la magia y la energía de los Nueve Reinos. Estas runas no se mueven de forma aleatoria, sino que están sometidas a las leyes físicas que rigen cada reino, creando un ecosistema dinámico y orgánico.

#### Cómo las fuerzas moldean las reglas de aceleración

#### Atracción Gravitacional (El Núcleo de Yggdrasil): 

Es la fuerza central de la obra. El árbol ejerce una atracción gravitacional constante sobre todas las runas, calculada mediante la constante gravitacional y la distancia. Esta regla garantiza que las runas nunca escapen del lienzo, manteniéndolas en una órbita perpetua.

#### Fricción (Las Nieblas de Niflheim): 

En la franja superior, las runas entran al reino del hielo y la niebla. La regla aquí dicta que experimenten una fuerza de fricción constante en dirección opuesta a su movimiento. Esto simula un aire denso y helado que reduce su aceleración paulatinamente.

#### Resistencia de Fluidos (El Pozo de Urd): 

En la franja inferior, las runas descienden a las aguas mágicas de las raíces. La regla matemática aquí es más agresiva: se aplica una fuerza de arrastre proporcional al cuadrado de la velocidad de la runa. Si una runa entra muy rápido, será frenada de golpe, simulando la densidad del agua.

#### Ruido de Perlin (Vientos Mágicos): 

Para evitar que las orbitas sean aburridas, una fuerza sutil basada en Ruido de Perlin empuja constantemente a las runas, simulando vientos orgánicos que alteran su inercia.

#### Interacción del Usuario: 

Al hacer clic, el usuario interviene como un dios, aplicando una fricción masiva universal que sobreescribe la velocidad de todas las runas, congelando el tiempo temporalmente.

#### Código de la aplicación 

```c
let runas = [];
let atractor;
let arbolBuffer; // Lienzo extra para dibujar a Yggdrasil una sola vez
const caracteresRunas = "ᚠᚢᚦᚬᚱᚴᚼᚽᚾᛅᛋᛏᛒᛘᛚᛦ"; 

function setup() {
  createCanvas(800, 600);
  
  // 1. Crear a Yggdrasil en un buffer de gráficos para no perder rendimiento
  arbolBuffer = createGraphics(800, 600);
  generarYggdrasil(arbolBuffer);
  
  // 2. Posicionamos el núcleo gravitacional justo en el tronco del árbol
  // FUERZA 1: ATRACCIÓN GRAVITACIONAL
  atractor = new Atractor(width / 2.3, height / 1.7, 30);
  
  // 3. Generamos las runas flotantes
  for (let i = 0; i < 80; i++) {
    let x = random(width);
    let y = random(height);
    let m = random(1, 3);
    runas.push(new Runa(x, y, m));
  }
}

function draw() {
  background(10, 15, 25, 80);

  // --- ZONAS VISUALES DE LOS REINOS ---
  // Zona de Fricción (Niflheim - Arriba)
  noStroke();
  fill(150, 200, 255, 20); // Tono escarcha
  rect(0, 0, width, 150);
  
  // Zona de Fluidos (Pozo de Urd - Abajo)
  fill(0, 100, 150, 30); // Tono agua profunda
  rect(0, height - 150, width, 150);

  // Dibujamos el árbol Yggdrasil estático
  image(arbolBuffer, 0, 0);

  for (let runa of runas) {
    // ---------------------------------------------------------
    // FUERZA 1: ATRACCIÓN GRAVITACIONAL (Hacia el centro)
    // ---------------------------------------------------------
    let fuerzaGravedad = atractor.atraer(runa);
    runa.aplicarFuerza(fuerzaGravedad);

    // ---------------------------------------------------------
    // FUERZA 2: FRICCIÓN (Nieblas de Niflheim - Parte Superior)
    // ---------------------------------------------------------
    if (runa.pos.y < 150) {
      let friccion = runa.vel.copy();
      friccion.normalize();
      friccion.mult(-1); // Dirección opuesta
      
      let mu = 0.1; // Coeficiente de fricción (constante)
      friccion.setMag(mu);
      runa.aplicarFuerza(friccion);
    }

    // ---------------------------------------------------------
    // FUERZA 3: RESISTENCIA DE FLUIDOS (Pozo de Urd - Parte Inferior)
    // ---------------------------------------------------------
    if (runa.pos.y > height - 150) {
      let drag = runa.vel.copy();
      drag.normalize();
      drag.mult(-1); // Dirección opuesta
      
      let c = 0.08; // Coeficiente de resistencia del fluido
      let speedSq = runa.vel.magSq(); // Velocidad al cuadrado
      drag.setMag(c * speedSq);
      
      runa.aplicarFuerza(drag);
    }

    // Vientos de Helheim (Ruido de Perlin) para dar movimiento orgánico
    let angle = noise(runa.pos.x * 0.005, runa.pos.y * 0.005, frameCount * 0.01) * TWO_PI * 2;
    let vientoPerlin = p5.Vector.fromAngle(angle);
    vientoPerlin.mult(0.1); 
    runa.aplicarFuerza(vientoPerlin);

    // Fricción interactiva al hacer clic (Congela todo)
    if (mouseIsPressed) {
      let friccionInteractiva = runa.vel.copy();
      friccionInteractiva.normalize();
      friccionInteractiva.mult(-1);
      friccionInteractiva.setMag(0.08);
      runa.aplicarFuerza(friccionInteractiva);
    }

    runa.actualizar();
    runa.mostrar();
  }
}

// --- FUNCIÓN RECURSIVA PARA YGGDRASIL ---
function generarYggdrasil(pg) {
  pg.stroke(150, 100, 200, 150); 
  pg.push();
  pg.translate(pg.width / 2, pg.height / 1.6);
  
  pg.drawingContext.shadowBlur = 20;
  pg.drawingContext.shadowColor = color(150, 100, 255);

  dibujarRama(pg, 90, 10); // Ramas
  pg.rotate(PI);
  dibujarRama(pg, 70, 8); // Raíces
  pg.pop();
}

function dibujarRama(pg, longitud, grosor) {
  pg.strokeWeight(grosor);
  pg.line(0, 0, 0, -longitud);
  pg.translate(0, -longitud);
  
  if (longitud > 8) {
    pg.push();
    pg.rotate(PI / 5);
    dibujarRama(pg, longitud * 0.7, grosor * 0.7);
    pg.pop();
    
    pg.push();
    pg.rotate(-PI / 5);
    dibujarRama(pg, longitud * 0.7, grosor * 0.7);
    pg.pop();
  }
}

// --- CLASES FÍSICAS ---

class Atractor {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.masa = m;
    this.G = 1.5; 
  }

  atraer(runa) {
    let fuerza = p5.Vector.sub(this.pos, runa.pos);
    let distancia = fuerza.mag();
    distancia = constrain(distancia, 15, 100); 
    fuerza.normalize();
    
    // Ley de gravitación universal
    let intensidad = (this.G * this.masa * runa.masa) / (distancia * distancia);
    fuerza.mult(intensidad);
    return fuerza;
  }
}

class Runa {
  constructor(x, y, m) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D().mult(random(2, 4)); 
    this.acc = createVector(0, 0);
    this.masa = m;
    this.simbolo = caracteresRunas.charAt(floor(random(caracteresRunas.length)));
  }

  aplicarFuerza(fuerza) {
    // Segunda ley de Newton: a = F / m
    let f = p5.Vector.div(fuerza, this.masa);
    this.acc.add(f);
  }

  actualizar() {
    this.vel.add(this.acc);
    this.vel.limit(6); 
    this.pos.add(this.vel);
    this.acc.mult(0); // Reseteo de aceleración
  }

  mostrar() {
    drawingContext.shadowBlur = 15;
    drawingContext.shadowColor = color(0, 255, 255);
    
    fill(200, 240, 255);
    noStroke();
    textSize(this.masa * 10); 
    textAlign(CENTER, CENTER);
    text(this.simbolo, this.pos.x, this.pos.y);
    
    drawingContext.shadowBlur = 0;
  }
}
````

#### Enlace del proyecto

https://editor.p5js.org/truji2506/sketches/UhyscnZZ4

#### Captura de pantalla

<img width="797" height="597" alt="image" src="https://github.com/user-attachments/assets/6689665b-589c-4d9b-bb38-a166a35aed99" />


## Bitácora de reflexión

#### Acividad 5

#### Enunciado

Explica detalladamente en tu bitácora ¿Qué es el marco de movimiento motion 101 y cómo se relacionan: fuerza, aceleración, velocidad y posición?
Vas a analizar este video sobre el artista Alexander Calder. Selecciona una de sus obras y luego crea una obra generativa inspirada en la obra de Calder que seleccionaste y el marco de movimiento motion 101 con fuerzas que trabajamos en esta unidad.

#### Solución 

#### 1. ¿Qué es el marco de movimiento motion 101 y cómo se relacionan: fuerza, aceleración, velocidad y posición?

En el marco 101 es la base algoritmica para simular la fisica realista en entornos donde se necesitan visuales usando p5.js, donde usando las fisicas le damos reglas fisicas y dejamos que el sistemas vaya calculando su posición.

En este marco pondera la segunda Ley de Newton y eso establece una cadena basado en 4 conceptos

#### Fuerza:

Es cualquier empuje o movimiento que afecta un objeto, esto consta de varias fuerza sea la gravedad, el viento y fricción donde se pueden sumar en un solo frame para obtener una fuerza neta

#### Aceleración:

Es el resultado de aplicar fuerza a un objeto con masa es lo que dice que tan rapido esta cambiando un objeto con respecto a la velocidad, en p5 la acceleración se va recalculando desde cero en cada frame 

#### Velocidad:

Esto va muy ligado a la aceleracion a lo largo del tiempo, esto nos dice hacia donde y que tan rapido se mueve el objeto en ese instante

#### Posición:

Es el punto en el espacio donde se encuentra el objeto, y este se va actualizando constantemente sumandole la velocidad actual

Todas las anteriores generan un ciclo constante, donde las fuerzas alteran la aceleración, la aceleración altera la velocidad, la velocidad altera la posición.

#### 2. Análisis de la Obra de Alexander Calder

La obra que me parecio mucho mas atractiva fue Red Mobile, donde el autor revolucionó el arte al introducir el movimiento fisico real, donde esta obra esta sometidas a fuerzas contantes

La Gravedad: Que tira de las placas de metal hacia el suelo.

La Tensión: El alambre estructural que ejerce una fuerza elástica (Ley de Hooke) hacia arriba, contrarrestando la gravedad para mantener las piezas suspendidas.

El Viento: Fuerzas aerodinámicas caóticas que interactúan con las formas planas, dándole a la escultura su movimiento orgánico e hipnótico.

#### 3. Obra Generativa Inspirada en Calder

Ya que Motion 101 trabaja con físicas lineales (vectores 2D) y no con cuerpos rígidos rotacionales complejos, he adaptado la escultura cinética de Calder usando Fuerzas de Resorte (Spring Forces).
Cada pieza del "móvil" digital está conectada por un resorte invisible a un punto de anclaje. Le aplicaremos la Gravedad (hacia abajo), la Tensión del Resorte (hacia el anclaje) y un Viento basado en Ruido de Perlin para que la escultura "respire" y se balancee suavemente. Utilizamos la paleta de colores primarios clásica de Calder.

#### Codigo 

```c
// Obra: "Móvil Cinético Generativo"
// Inspiración: Alexander Calder + Motion 101

let piezas = [];
let resortes = [];

function setup() {
  createCanvas(800, 600);
  
  // Creamos 3 puntos de anclaje en el techo
  let anclaje1 = createVector(width/2 - 150, 50);
  let anclaje2 = createVector(width/2, 50);
  let anclaje3 = createVector(width/2 + 150, 50);

  // Creamos las piezas del móvil (formas abstractas de Calder)
  // Parámetros Mover: x, y, masa, color
  let p1 = new Mover(width/2 - 150, 300, 4, color(220, 30, 30)); // Rojo
  let p2 = new Mover(width/2, 400, 2, color(30, 30, 220));      // Azul
  let p3 = new Mover(width/2 + 150, 250, 6, color(240, 200, 30)); // Amarillo
  
  piezas.push(p1, p2, p3);

  // Creamos los resortes conectando cada pieza a su anclaje
  // Parámetros Spring: anclaje, longitud de reposo, constante elástica (k)
  resortes.push(new Spring(anclaje1, 200, 0.05));
  resortes.push(new Spring(anclaje2, 250, 0.02)); // Resorte más largo y suave
  resortes.push(new Spring(anclaje3, 150, 0.1));  // Resorte rígido y corto
}

function draw() {
  background(245, 240, 235); // Fondo de galería de arte

  // Calcular el viento usando Perlin Noise
  // Esto le da el movimiento orgánico característico de un móvil
  let nx = noise(frameCount * 0.005) - 0.5; // Valores entre -0.5 y 0.5
  let viento = createVector(nx * 0.5, 0);

  for (let i = 0; i < piezas.length; i++) {
    let pieza = piezas[i];
    let resorte = resortes[i];

    // FUERZA 1: Gravedad
    let gravedad = createVector(0, 0.2 * pieza.masa);
    pieza.aplicarFuerza(gravedad);

    // FUERZA 2: Viento (Ruido de Perlin)
    pieza.aplicarFuerza(viento);

    // FUERZA 3: Tensión del resorte (Ley de Hooke)
    resorte.conectar(pieza);

    // FUERZA 4: Fricción del aire (para que no reboten infinitamente)
    let friccion = pieza.vel.copy();
    friccion.normalize();
    friccion.mult(-1);
    friccion.setMag(0.05); // Resistencia del aire de la galería
    pieza.aplicarFuerza(friccion);

    // Mostrar todo
    resorte.mostrarLineas(pieza);
    pieza.actualizar();
    pieza.mostrar(i);
  }
}

// --- CLASES DEL MARCO MOTION 101 ---

class Spring {
  constructor(anclaje, longitud, k) {
    this.anclaje = anclaje;
    this.restLength = longitud;
    this.k = k; // Constante del resorte (rigidez)
  }

  conectar(mover) {
    // Ley de Hooke: F = -k * x
    let fuerza = p5.Vector.sub(mover.pos, this.anclaje);
    let d = fuerza.mag();
    let estiramiento = d - this.restLength;

    fuerza.normalize();
    fuerza.mult(-1 * this.k * estiramiento); // Empujar o jalar dependiendo del estiramiento
    
    mover.aplicarFuerza(fuerza);
  }

  mostrarLineas(mover) {
    stroke(50);
    strokeWeight(1.5);
    line(mover.pos.x, mover.pos.y, this.anclaje.x, this.anclaje.y);
    // Dibujar el punto de anclaje
    fill(50);
    noStroke();
    circle(this.anclaje.x, this.anclaje.y, 8);
  }
}

class Mover {
  constructor(x, y, m, c) {
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.masa = m;
    this.color = c;
  }

  aplicarFuerza(fuerza) {
    let f = p5.Vector.div(fuerza, this.masa);
    this.acc.add(f);
  }

  actualizar() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.acc.mult(0);
  }

  mostrar(index) {
    fill(this.color);
    noStroke();
    
    // Dibujamos diferentes formas geométricas para emular a Calder
    push();
    translate(this.pos.x, this.pos.y);
    if (index === 0) {
      ellipse(0, 0, this.masa * 16, this.masa * 12); // Óvalo
    } else if (index === 1) {
      triangle(-this.masa*8, this.masa*8, 0, -this.masa*10, this.masa*8, this.masa*8); // Triángulo
    } else {
      circle(0, 0, this.masa * 15); // Círculo
    }
    pop();
  }
}
````






