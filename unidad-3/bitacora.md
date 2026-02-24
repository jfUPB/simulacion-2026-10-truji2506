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


## Bitácora de reflexión




