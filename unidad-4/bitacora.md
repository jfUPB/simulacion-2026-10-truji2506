# Unidad 4

## Bitácora de proceso de aprendizaje

#### Acividad 1

#### Enunciado

Documenta en tu bitácora de aprendizaje los aspectos que más te llamaron la atención de la obra de Memo.

##  Solución

Utiliza la función sinusoide básica, pero al desfasar múltiples formas y superponerlas, elimina la sensación de que estamos viendo una simulación. La obra respira y fluye, demostrando que el diseño, la repetición operativa genera resultados organicos.

#### Acividad 2

#### Enunciado

Documenta en tu bitácora de aprendizaje las respuestas a las preguntas anteriores.

##  Solución

¿Qué pasa en la simulación y el origen (0,0)? 

El punto (0,0) está en la esquina superior izquierda. Al usar translate(width/2, height/2), movemos ese papel virtual para que el centro de la pantalla sea el nuevo (0,0). Hacemos esto porque la función rotate() siempre gira todo el lienzo alrededor del origen. Si dibujamos las figuras en (0,0) después de trasladar el lienzo, las figuras girarán perfectamente sobre su propio centro, como una rueda.

¿Qué hace heading()? 

Calcula el ángulo de rotación de un vector en radianes. Matemáticamente, resuelve el ángulo usando $\theta = \arctan(y / x)$ basándose en la velocidad actual.¿Qué hacen push() y pop()? Son salvavidas. push() guarda el estado actual del sistema de coordenadas, y pop() lo restaura. Sin ellos, si rotas un cuadrado 45 grados, el siguiente elemento que dibujes también saldrá rotado. Aislan las transformaciones.

¿Qué hace rectMode(CENTER)? 

Cambia el punto de anclaje de un rectángulo. En lugar de dibujarse desde la esquina superior izquierda, se dibuja desde su centro exacto, vital para que la rotación se vea natural.

#### Acividad 3

#### Enunciado

Documenta en tu bitácora de aprendizaje tu proceso de creación de la simulación.

##  Solución

Codigo del ejercicio 

```c
let vehiculo;

function setup() {
  createCanvas(600, 400);
  vehiculo = new Vehiculo(width / 2, height / 2);
}

function draw() {
  background(240);
  
  // Ejecutamos los métodos de nuestro vehículo en orden
  vehiculo.controlar();     // 1. Leer el teclado
  vehiculo.actualizar();    // 2. Aplicar las matemáticas (Motion 101)
  vehiculo.revisarBordes(); // 3. Hacer que aparezca por el otro lado si sale de la pantalla
  vehiculo.mostrar();       // 4. Dibujar en pantalla
}

// --- CLASE VEHÍCULO ---
class Vehiculo {
  constructor(x, y) {
    this.posicion = createVector(x, y);
    this.velocidad = createVector(0, 0);
    this.aceleracion = createVector(0, 0);
    this.velocidadMaxima = 6; // Límite para que no se vuelva incontrolable
  }

  // Detecta las flechas del teclado y aplica una fuerza de aceleración
  controlar() {
    let fuerza = createVector(0, 0);
    
    if (keyIsDown(LEFT_ARROW)) {
      fuerza.x = -0.3; // Acelera a la izquierda
    }
    if (keyIsDown(RIGHT_ARROW)) {
      fuerza.x = 0.3;  // Acelera a la derecha
    }
    if (keyIsDown(UP_ARROW)) {
      fuerza.y = -0.3; // Acelera hacia arriba
    }
    if (keyIsDown(DOWN_ARROW)) {
      fuerza.y = 0.3;  // Acelera hacia abajo
    }
    
    // Sumamos la fuerza del teclado a la aceleración actual
    this.aceleracion.add(fuerza);
  }

  // El corazón de Motion 101
  actualizar() {
    this.velocidad.add(this.aceleracion);
    this.velocidad.limit(this.velocidadMaxima);
    this.posicion.add(this.velocidad);
    
    // Si no estamos presionando ninguna tecla, aplicamos una "fricción"
    // para que la nave se detenga suavemente (opcional pero se siente mejor)
    this.velocidad.mult(0.98); 
    
    this.aceleracion.mult(0); // Reseteo obligatorio en cada frame
  }

  mostrar() {
    // Magia de la trigonometría: heading() calcula el ángulo de la velocidad
    let angulo = this.velocidad.heading();

    push(); // Guardamos el estado del canvas
    translate(this.posicion.x, this.posicion.y); // Nos movemos a la posición de la nave
    rotate(angulo); // Rotamos el canvas según la dirección del movimiento
    
    fill(50, 150, 255);
    stroke(0);
    strokeWeight(2);
    
    // Dibujamos un triángulo apuntando hacia la derecha (0 radianes)
    // Coordenadas: (Punta trasera arriba), (Punta delantera), (Punta trasera abajo)
    triangle(-15, -10, 15, 0, -15, 10); 
    
    pop(); // Restauramos el canvas
  }

  // Efecto Pac-Man: Si sale por un borde, entra por el opuesto
  revisarBordes() {
    if (this.posicion.x > width + 15) this.posicion.x = -15;
    if (this.posicion.x < -15) this.posicion.x = width + 15;
    if (this.posicion.y > height + 15) this.posicion.y = -15;
    if (this.posicion.y < -15) this.posicion.y = height + 15;
  }
}
```

#### Acividad 4

#### Enunciado

Documenta en tu bitácora de aprendizaje las respuestas a las preguntas anteriores.

##  Solución

Codigo del ejercicio

```c
let movers = [];
let attractor;

function setup() {
  createCanvas(640, 360);
  
  // Creamos varios "Movers" (los elementos que son atraídos)
  for (let i = 0; i < 10; i++) {
    movers[i] = new Mover(random(width), random(height), random(0.5, 3));
  }
  
  // Instanciamos el atractor en el centro
  attractor = new Attractor();
}

function draw() {
  background(240);

  // 1. Verificamos la interacción del mouse con el atractor
  attractor.verificarHover(mouseX, mouseY);
  attractor.arrastrar(mouseX, mouseY);
  attractor.mostrar();

  // 2. Aplicamos la fuerza de atracción a cada mover
  for (let i = 0; i < movers.length; i++) {
    let force = attractor.atraer(movers[i]);
    movers[i].aplicarFuerza(force);
    movers[i].actualizar();
    movers[i].mostrar();
  }
}

// --- FUNCIONES NATIVAS DE P5.JS PARA EL MOUSE ---
// Estas funciones se activan automáticamente cuando haces clic o sueltas el mouse
function mousePressed() {
  attractor.presionarClic(mouseX, mouseY);
}

function mouseReleased() {
  attractor.soltarClic();
}


// ==========================================
// CLASE ATTRACTOR (El núcleo interactivo)
// ==========================================
class Attractor {
  constructor() {
    this.posicion = createVector(width / 2, height / 2);
    this.masa = 20;
    this.G = 1; // Constante gravitacional
    
    // Variables para la interacción
    this.offsetArrastre = createVector(0, 0);
    this.dragging = false; // ¿Lo estoy arrastrando?
    this.rollover = false; // ¿Tengo el mouse encima?
  }

  atraer(mover) {
    let fuerza = p5.Vector.sub(this.posicion, mover.posicion);
    let d = fuerza.mag();
    d = constrain(d, 5, 25);
    fuerza.normalize();
    let magnitudFuerza = (this.G * this.masa * mover.masa) / (d * d);
    fuerza.mult(magnitudFuerza);
    return fuerza;
  }

  mostrar() {
    ellipseMode(CENTER);
    strokeWeight(4);
    stroke(0);
    
    // Aquí cambiamos el color dependiendo del estado (Respuesta a la Actividad)
    if (this.dragging) {
      fill(50); // Gris muy oscuro si lo estoy arrastrando
    } else if (this.rollover) {
      fill(100); // Gris medio si solo tengo el cursor encima
    } else {
      fill(175, 200); // Gris claro por defecto
    }
    
    circle(this.posicion.x, this.posicion.y, this.masa * 2);
  }

  // --- MÉTODOS DE INTERACCIÓN ---

  // Verifica si el mouse está sobre el círculo
  verificarHover(mx, my) {
    let d = dist(mx, my, this.posicion.x, this.posicion.y);
    if (d < this.masa) {
      this.rollover = true;
    } else {
      this.rollover = false;
    }
  }

  // Se activa desde mousePressed()
  presionarClic(mx, my) {
    if (this.rollover) {
      this.dragging = true;
      // Guardamos la diferencia entre donde hice clic y el centro real del círculo
      // para que al arrastrarlo no "salte" al cursor bruscamente
      this.offsetArrastre.x = this.posicion.x - mx;
      this.offsetArrastre.y = this.posicion.y - my;
    }
  }

  // Se activa constantemente en el draw() si dragging es true
  arrastrar(mx, my) {
    if (this.dragging) {
      this.posicion.x = mx + this.offsetArrastre.x;
      this.posicion.y = my + this.offsetArrastre.y;
    }
  }

  // Se activa desde mouseReleased()
  soltarClic() {
    this.dragging = false;
  }
}


// ==========================================
// CLASE MOVER (El marco Motion 101)
// ==========================================
class Mover {
  constructor(x, y, m) {
    this.masa = m;
    this.posicion = createVector(x, y);
    this.velocidad = createVector(0, 0);
    this.aceleracion = createVector(0, 0);
  }

  aplicarFuerza(fuerza) {
    // a = F / m
    let f = p5.Vector.div(fuerza, this.masa);
    this.aceleracion.add(f);
  }

  actualizar() {
    this.velocidad.add(this.aceleracion);
    this.posicion.add(this.velocidad);
    
    // RESPUESTA A LA ACTIVIDAD: Modificación vital de Motion 101
    // Sin esto, la aceleración se sumaría infinitamente en cada frame
    this.aceleracion.mult(0); 
  }

  mostrar() {
    stroke(0);
    strokeWeight(2);
    fill(0, 150, 255, 150); // Un tono azulado para diferenciarlos del atractor
    circle(this.posicion.x, this.posicion.y, this.masa * 16);
  }
}
```
#### Acividad 5  

#### Enunciado

Documenta en tu bitácora de aprendizaje las respuestas a las preguntas anteriores.

##  Solución

#### Acividad 6

#### Enunciado

Documenta tus reflexiones sobre la función sinusoide en tu bitácora de aprendizaje.

##  Solución

#### Acividad 7

#### Enunciado

Documenta en tu bitácora de aprendizaje el proceso de modificación de la simulación.

##  Solución

#### Acividad 8  

#### Enunciado

Documenta en tu bitácora de aprendizaje el proceso de modificación de la simulación.

##  Solución

#### Acividad 9  

#### Enunciado

Documenta en tu bitácora de aprendizaje el proceso de modificación de la simulación.

##  Solución

#### Acividad 10 

#### Enunciado

Documenta en tu bitácora de aprendizaje el proceso de modificación de la simulación.

##  Solución

## Bitácora de aplicación 

#### Acividad 11  

#### Enunciado

1. Describe el concepto de tu obra generativa. Recuerda que desde la unidad anterior añadimos la idea de narrativa a la obra generativa, para guiar algunas de las decisiones en la definición de reglas del sistema generativo. PERO OJO, no estamos contando una historia, estamos usando la narrativa como herramienta de diseño para la definición de reglas.
2. El código de la aplicación.
3. Un enlace al proyecto en el editor de p5.js.
4. Selecciona capturas de pantalla representativas de tu pieza de arte generativa.

##  Solución

## Bitácora de reflexión

#### Acividad 12  

#### Enunciado

Documenta tu diagrama conceptual en tu bitácora de aprendizaje.

##  Solución


