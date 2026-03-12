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
  
  vehiculo.controlar();   
  vehiculo.actualizar();    
  vehiculo.revisarBordes(); 
  vehiculo.mostrar();       
}

// --- CLASE VEHÍCULO ---
class Vehiculo {
  constructor(x, y) {
    this.posicion = createVector(x, y);
    this.velocidad = createVector(0, 0);
    this.aceleracion = createVector(0, 0);
    this.velocidadMaxima = 6; 
  }

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
    this.aceleracion.add(fuerza);
  }

  // El corazón de Motion 101
  actualizar() {
    this.velocidad.add(this.aceleracion);
    this.velocidad.limit(this.velocidadMaxima);
    this.posicion.add(this.velocidad);
    this.velocidad.mult(0.98); 
    
    this.aceleracion.mult(0); 
  }

  mostrar() {
    let angulo = this.velocidad.heading();

    push(); 
    translate(this.posicion.x, this.posicion.y);
    rotate(angulo); 
    
    fill(50, 150, 255);
    stroke(0);
    strokeWeight(2);
    triangle(-15, -10, 15, 0, -15, 10); 
    
    pop();
  }

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
  
  for (let i = 0; i < 10; i++) {
    movers[i] = new Mover(random(width), random(height), random(0.5, 3));
  }

  attractor = new Attractor();
}

function draw() {
  background(240);

  attractor.verificarHover(mouseX, mouseY);
  attractor.arrastrar(mouseX, mouseY);
  attractor.mostrar();

  for (let i = 0; i < movers.length; i++) {
    let force = attractor.atraer(movers[i]);
    movers[i].aplicarFuerza(force);
    movers[i].actualizar();
    movers[i].mostrar();
  }
}

function mousePressed() {
  attractor.presionarClic(mouseX, mouseY);
}

function mouseReleased() {
  attractor.soltarClic();
}

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

    if (this.dragging) {
      fill(50); // Gris muy oscuro si lo estoy arrastrando
    } else if (this.rollover) {
      fill(100); // Gris medio si solo tengo el cursor encima
    } else {
      fill(175, 200); // Gris claro por defecto
    }
    
    circle(this.posicion.x, this.posicion.y, this.masa * 2);
  }

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



