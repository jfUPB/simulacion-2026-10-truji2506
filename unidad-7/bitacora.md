# Unidad 7

## Bitácora de proceso de aprendizaje
#### Acividad 1

#### Enunciado

Explica con tus palabras qué hace cada uno de esos conceptos.
Replica al menos dos experimentos básicos integrando Matter.js con p5.js.
Incluye código y capturas o enlaces.
Describe qué tipo de comportamiento físico te interesa explorar en tu palabra.

##  Solución

MOON: Lee utiliza las letras "O" para crear una interacción espacial. Una "O" es grande (la luna o la tierra) y la otra es pequeña y orbita a su alrededor como un satélite.

EXIT: La letra "X" sufre una modificación en sus vértices, transformándose en una figura humana que corre hacia la salida, interactuando con la "I" como si fuera una puerta.

IDEA: Se invierte la letra "i" minúscula. Al voltearla, el punto y el tallo forman visualmente un foco o bombillo encendido, todo con la misma tipografía original.
Explicación: En todos estos casos, la manipulación tipográfica refuerza el significado porque rompe la lectura tradicional lineal. La letra deja de ser solo un código fonético para convertirse en un objeto visual que actúa su propio significado.

#### Acividad 2

#### Enunciado

Explica con tus palabras qué hace cada uno de esos conceptos.
Replica al menos dos experimentos básicos integrando Matter.js con p5.js.
Incluye código y capturas o enlaces.
Describe qué tipo de comportamiento físico te interesa explorar en tu palabra.

##  Solución

Experimento 1: Creé varios Bodies.circle que caen afectados por la gravedad y chocan contra un Bodies.rectangle estático (el suelo).

Experimento 2: Usé un Constraint.create para unir un círculo dinámico a un punto fijo en el techo, observando cómo la inercia afecta el movimiento.

#### Acividad 3

#### Enunciado

Realiza al menos dos experimentos simples de audio-reactividad.
Explica qué dato estás leyendo del audio.
Explica qué comportamiento visual o físico activa ese dato.
Describe qué tipo de respuesta sonora te serviría más para tu palabra y por qué.

##  Solución

Para "MILPA", la respuesta sonora que más me sirve es el evento puntual por umbral (Soplido). No quiero que el fuego simplemente "baile" con la música. Quiero que la pieza tenga una interacción performativa: cuando el usuario genera un sonido fuerte (un soplido al micrófono), ese evento físico detona el cambio de estado definitivo en el sistema de partículas, apagando el fuego y convirtiendo todo en ceniza muerta.

#### Acividad 4

#### Enunciado

Muestra una prueba inicial.
Explica qué parte de la palabra construiste.
Explica qué propiedad física manipulaste.
Explica qué aspecto del audio afecta qué comportamiento.
Evalúa qué funcionó y qué no para el significado que quieres construir.

##  Solución

Prueba Inicial:
Desarrollé un prototipo donde la palabra "MILPA" se muestra en dos formas superpuestas: una capa sólida renderizada con una máscara de recorte (clip()) y un sistema de partículas generadas a partir de los puntos del contorno tipográfico (textToPoints).

Parte de la palabra construida: Toda la palabra "MILPA" como un sistema integrado. Inicia con la rigidez de la fuente Rubik Dirt y se descompone en cientos de partículas independientes.

Propiedad física manipulada: Manipulé las fuerzas vectoriales. Apliqué Ruido de Perlin para simular la turbulencia termodinámica del fuego y levantamiento negativo (para que las llamas suban). Además, apliqué la fuerza de Arrive (Llegada) para que, tras ser esparcidas por el viento, las cenizas busquen regresar y mantenerse en la forma de la letra.

Aspecto del audio: Utilicé el volumen continuo (amplitud) para activar el viento. Cuando mic.getLevel() supera el umbral, se aplica una fuerza aleatoria (una ráfaga de p5.Vector.random2D()) que vence la fuerza de llegada de las partículas, esparciéndolas dramáticamente por el canvas.

Evaluación del significado construido:

¿Qué funcionó? La transición estocástica. El contraste entre la letra vectorizada perfecta y el caos orgánico del ruido de Perlin comunica perfectamente la destrucción de la fachada corporativa. La fuerza de Arrive es un éxito: hace que la ceniza se sienta pesada y atada a su realidad (el carbón).

¿Qué no funcionó inicialmente? Al principio, las partículas vibraban demasiado y se perdía la legibilidad de la palabra de inmediato. Tuve que ajustar la magnitud de la fuerza de Arrive para equilibrar el caos del fuego con la retención de la forma, logrando que la palabra se siga leyendo mientras se quema.


## Bitácora de aplicación 

#### Acividad 5

#### Enunciado

Palabra elegida.
Justificación conceptual.
Análisis de su significado visual y comportamental.
Moodboard o referencias.
Bocetos.
Mapa de decisiones.
Mapa de interpretación.
Explicación de la relación entre audio y comportamiento.
Evidencia del uso de IA.
Código fuente.
Enlace al sketch.
Capturas o registros de la pieza.

##  Solución


1. MILPA (en transición conceptual y material hacia su realidad física: el Carbón).

2. Existe una empresa minera dedicada a la extracción de carbón bajo el nombre de "Milpa". Históricamente, una milpa es un agroecosistema mesoamericano que representa la vida, el sustento y la tierra fértil. Apropiarse de esta palabra para nombrar la extracción fósil es una contradicción profunda.
La pieza busca revelar la verdad material detrás de la fachada corporativa: la palabra se presenta sólida, pero es inestable. Al someterse a la energía (el fuego) y a la interacción humana (el soplido del espectador), la fachada verde y prístina se consume para dejar a la vista su única realidad física: cenizas y residuo mineral.

3. Visual: Inicio con un estado rígido, pesado y oscuro. El uso de la tipografía Rubik Dirt y la máscara de recorte (clip()) hace que la palabra nazca como un bloque de carbón poroso.

Comportamental: La transición de sólido a energía (fuego) y luego a residuo (ceniza) se logra pasando de un renderizado estático a un sistema dinámico de Agentes Autónomos. Las partículas de fuego se comportan con turbulencia termodinámica (Perlin Noise), mientras que la ceniza se comporta bajo la inercia y el peso, buscando su forma inerte mediante fuerzas de dirección (Steering behaviors: Arrive).

8. El audio en esta pieza no es un simple ecualizador decorativo ("que el fuego baile con la música"). Actúa como un gatillo narrativo.
El volumen continuo (mic.getLevel()) es leído por el sistema en segundo plano, pero solo cobra vida semántica cuando el usuario realiza un soplido intencional que supera el límite de ignición. Este pico de audio detona un cambio de estado en la máquina de estados: anula la variable ardiendo, cambia el mapeo de color a grises e inyecta una explosión vectorial que simboliza la dispersión de la ceniza por el viento, cortando el sonido pregrabado del fuego bruscamente.

9. Decisiones de Autoría Conceptual (Propias):

La elección de la palabra MILPA y su trasfondo de greenwashing minero.

El concepto de transmutación: de sólido a fuego, de fuego a ceniza.

El diseño de interacción de 4 actos (espera, clic/chispa, fuego, soplido/apagado).

Uso de IA como apoyo técnico (Materializador):

Utilicé IA (Gemini) para resolver problemas sintácticos en p5.js, específicamente para generar el algoritmo de centrado dinámico de textToPoints utilizando font.textBounds().

La IA funcionó como traductor entre mis ideas y el código: le propuse mi concepto de destrucción y, apoyado en el libro The Nature of Code, la IA estructuró la lógica matemática del comportamiento Arrive y el ruido de Perlin para evitar la saturación de memoria de usar un motor de cuerpos rígidos como Matter.js para miles de partículas.

10. 

Sketch.js

```c
let font;
let particulas = [];
let puntosMilpa = [];
let sndCandela;
let sndFuego;
let mic;
let estado = "CARBON"; 
let umbralSoplido = 0.15; 
let limiteIgnicion = 0;   
let boundingBox; 
let tamañoTexto = 250; 
let textoMilpa = 'MILPA';
let startX, startY; 

function preload() {
  font = loadFont('RubikDirt-Regular.ttf'); 
  sndCandela = loadSound('freesound_community-boosted_flick_clipper-45800.mp3');
  sndFuego = loadSound('freesounds123-fire-340951.mp3');     
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  
  userStartAudio(); 
  mic = new p5.AudioIn();
  mic.start();
  
  generarParticulas();
}

function generarParticulas() {
  particulas = []; 
  boundingBox = font.textBounds(textoMilpa, 0, 0, tamañoTexto);
  startX = (width / 2) - (boundingBox.w / 2);
  startY = (height / 2) + (boundingBox.h / 2) - 50; 
  
  let opcionesMilpa = { sampleFactor: 0.25, simplifyThreshold: 0 };
  puntosMilpa = font.textToPoints(textoMilpa, startX, startY, tamañoTexto, opcionesMilpa);
  
  let minX = width;
  for (let i = 0; i < puntosMilpa.length; i++) {
    if (puntosMilpa[i].x < minX) minX = puntosMilpa[i].x;
  }
  limiteIgnicion = minX - 10; 
  
  for (let i = 0; i < puntosMilpa.length; i++) {
    let pt = puntosMilpa[i];
    particulas.push(new Particula(pt.x, pt.y));
  }
}

function draw() {
  background(247, 247, 247); 
  
  let vol = mic.getLevel();
  if (estado === "ENCENDIENDO") {
    limiteIgnicion += 15; 
    let todasEncendidas = true;
    
    for (let i = 0; i < particulas.length; i++) {
      let p = particulas[i];
      if (p.origen.x < limiteIgnicion) {
        p.ardiendo = true;
      }
      if (!p.ardiendo) todasEncendidas = false;
    }
    if (todasEncendidas) {
      estado = "FUEGO";
    }
  } 
  else if (estado === "FUEGO") {
    if (vol > umbralSoplido) {
      estado = "CENIZA";
      sndFuego.fade(0, 1.5); 
      setTimeout(() => sndFuego.stop(), 1500);
      
      for (let i = 0; i < particulas.length; i++) {
        particulas[i].ardiendo = false;
        particulas[i].esCeniza = true;
        
        let rafaga = p5.Vector.random2D();
        rafaga.mult(random(5, 20)); 
        particulas[i].applyForce(rafaga);
      }
    }
  }
  
  if (estado === "CARBON" || estado === "ENCENDIENDO" || estado === "FUEGO") {
    push();

    drawingContext.beginPath();
    let anchoRestante = width - limiteIgnicion;
    if (anchoRestante > 0) {
      drawingContext.rect(limiteIgnicion, 0, anchoRestante, height);
      drawingContext.clip();
      
      fill(35); 
      noStroke();
      textFont(font);
      textSize(tamañoTexto);
      textAlign(LEFT, BASELINE);
      text(textoMilpa, startX, startY);
    }
    pop();
  }

  for (let i = 0; i < particulas.length; i++) {
    let p = particulas[i];
    p.comportamientos();
    p.update();
    p.show();
  }
}

function mousePressed() {
  userStartAudio(); 
  
  if (estado === "CARBON") {
    estado = "ENCENDIENDO";
    if (sndCandela.isLoaded()) sndCandela.play();
    
    setTimeout(() => {
      if (sndFuego.isLoaded()) {
        sndFuego.loop();
        sndFuego.setVolume(0.5); 
      }
    }, 500); 
  }
}

function keyPressed() {
  if (key === 'f' || key === 'F') {
    let fs = fullscreen();
    fullscreen(!fs);
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  generarParticulas();
}

class Particula {
  constructor(x, y) {
    this.origen = createVector(x, y);
    this.pos = createVector(x, y);
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    
    this.maxSpeed = 8;
    this.maxForce = 0.5;
    
    this.ardiendo = false;
    this.esCeniza = false;
    this.noiseOffset = random(1000);
    
    this.radioBase = random(1.5, 3.5); 
  }
  
  comportamientos() {
    let fuerzaRegreso = this.arrive(this.origen);
    fuerzaRegreso.mult(1.0); 
    this.applyForce(fuerzaRegreso);
  
    if (this.ardiendo) {
      let angulo = map(noise(this.noiseOffset), 0, 1, 0, TWO_PI);
      let vibracionFuego = p5.Vector.fromAngle(angulo);
      vibracionFuego.mult(3.0); 
      
      let levitacionTermica = createVector(0, -1.5); 
      
      this.applyForce(vibracionFuego);
      this.applyForce(levitacionTermica);
      this.noiseOffset += 0.15; 
    }
  }
  
  arrive(target) {
    let desired = p5.Vector.sub(target, this.pos);
    let d = desired.mag();
    let speed = this.maxSpeed;
    
    if (d < 50) {
      speed = map(d, 0, 50, 0, this.maxSpeed);
    }
    
    desired.setMag(speed);
    let steer = p5.Vector.sub(desired, this.vel);
    steer.limit(this.maxForce);
    return steer;
  }
  
  applyForce(force) {
    this.acc.add(force);
  }
  
  update() {
    this.vel.add(this.acc);
    this.pos.add(this.vel);
    this.vel.mult(0.85); 
    this.acc.mult(0);
  }
  
  show() {
    noStroke();
    
    if (this.esCeniza) {
      fill(160, 160, 160, 180);
      circle(this.pos.x, this.pos.y, this.radioBase);
    } 
    else if (this.ardiendo) {
      let r = map(noise(this.noiseOffset), 0, 1, 220, 255);
      let g = map(noise(this.noiseOffset + 100), 0, 1, 60, 160);
      
      fill(r, g, 0, 40);
      circle(this.pos.x, this.pos.y, this.radioBase * 4.5);
      
      fill(r, g + 50, 50, 220);
      circle(this.pos.x, this.pos.y, this.radioBase * 1.5); 
    } 
  }
}
```

Index.html

```c
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Simbiosis Semántica: Milpa a Carbón</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/p5.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.9.0/addons/p5.sound.min.js"></script>
  <style>
    body { 
      margin: 0; 
      padding: 0; 
      overflow: hidden; 
      background-color:#ffffff; /* Fondo oscuro */
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
  </style>
</head>
<body>
  <script src="sketch.js"></script>
</body>
</html>
```

11. 

https://editor.p5js.org/truji2506/sketches/b2hFhDDGF

12.

Fase 1 
<img width="1632" height="695" alt="image" src="https://github.com/user-attachments/assets/5223247c-1cf7-498f-bacc-639db5e9fa7c" />

Fase 2 
<img width="1626" height="690" alt="image" src="https://github.com/user-attachments/assets/fa9e5e44-bb32-4d74-9760-d01c936914ed" />

Fase 3 
<img width="1283" height="518" alt="image" src="https://github.com/user-attachments/assets/286aa870-630d-4014-9b5a-c425f38018b9" />




## Bitácora de reflexión
