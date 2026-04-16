# Unidad 6

## Bitácora de proceso de aprendizaje
#### Acividad 1

#### Enunciado

Selecciona dos imágenes o piezas de Tyler Hobbs que te llamen la atención.
Describe qué decisiones visuales reconoces en ellas:
composición,
densidad,
dirección del movimiento,
color,
ritmo,
repetición y variación.
Explica por qué esas decisiones te parecen potentes.
Escribe una hipótesis: ¿Qué tipo de reglas o sistema crees que podrían estar detrás de esa pieza?

##  Solución

#### Acividad 2

#### Enunciado

Explica con tus propias palabras qué es un agente autónomo.
Explica qué es una steering force.
Compara una steering force con una fuerza externa como la gravedad.
Describe por qué estas ideas son útiles para diseñar comportamiento visual y no solo para simular movimiento.

##  Solución

#### Acividad 3

#### Enunciado

¿Cómo está construido el campo de flujo?
¿Qué representa cada celda o vector del campo?
¿Cómo usa un agente su posición para consultar el campo?
¿Cómo se convierte el vector consultado en una decisión de movimiento?
Identifica parámetros importantes del sistema, por ejemplo:
resolución,
maxspeed,
maxforce,
cantidad de agentes.
Realiza al menos una modificación y analiza el efecto visual que produce.
Además, responde:

¿Qué tipo de movimiento produce este algoritmo?
¿Qué sensaciones visuales te sugiere?
¿En qué tipo de pieza musical imaginas que podría funcionar bien?

##  Solución

#### Acividad 4

#### Enunciado

Explica con tus palabras las tres reglas básicas:
separación,
alineación,
cohesión.
Identifica qué parámetros controlan estas reglas.
Modifica uno o más pesos del sistema y describe el efecto visual y colectivo.
Describe el comportamiento emergente observado:
compacto,
disperso,
estable,
nervioso,
caótico,
fluido.
Además, responde:

¿Qué atmósfera visual produce el flocking?
¿En qué tipo de relación con una canción podría funcionar mejor este algoritmo?

##  Solución

#### Acividad 5

#### Enunciado

Explica con tus palabras las tres reglas básicas:
separación,
alineación,
cohesión.
Identifica qué parámetros controlan estas reglas.
Modifica uno o más pesos del sistema y describe el efecto visual y colectivo.
Describe el comportamiento emergente observado:
compacto,
disperso,
estable,
nervioso,
caótico,
fluido.
Además, responde:

¿Qué atmósfera visual produce el flocking?
¿En qué tipo de relación con una canción podría funcionar mejor este algoritmo?

##  Solución


## Bitácora de aplicación 

#### Acividad 6

#### Enunciado

Documenta el proceso completo:

Concepto visual.
Relación entre la visual y la canción.
Moodboard o referencias.
Dos o más bocetos.
Mapa de decisiones.
Mapa de interpretación.
Justificación del algoritmo elegido.
Explicación de la relación audio-visual.
Evidencia del uso de IA.
Código fuente.
Enlace al sketch.
Capturas o registros de momentos importantes de la pieza.


##  Solución

#### 1. Concepto visual.

Visualmente, Ascend es como mirar un océano vivo a través de un microscopio. El concepto central es un viaje de nueve minutos, exactamente lo que dura la canción.

Empezamos en lo más profundo del mar, en un ambiente oscuro y pesado. Pero a medida que la música avanza, vamos 'ascendiendo'. Lo que ven en pantalla no son simples puntos de código, sino formas que actúan como células vivas: respiran, se agrupan y mutan con los bajos del audio, hasta que al final rompemos la superficie en una explosión de colores luminosos y cálidos.

#### 2. Relación entre la visual y la canción.

Para integrar la música, mi objetivo era que el programa sintiera la curva narrativa de la canción. Dividí la experiencia visual en dos momentos: Tensión y Liberación.

Durante la fase de Tensión, la energía de los bajos altera directamente las matemáticas del código, haciendo que las células se muevan más rápido y brillen más. Pero para la fase de Liberación, programé un evento exacto. En el minuto 6:02, que es el 'drop' de la pista, el algoritmo inyecta una fuerza caótica que destruye el orden de la corriente y cambia instantáneamente la paleta de colores. El código acompaña el viaje emocional de la música de principio a fin.

#### 3. Moodboard o referencias.

<img width="1173" height="657" alt="Referencia visual 1 (Video Rufus Du Sol)" src="https://github.com/user-attachments/assets/19a68152-8652-4d0c-b880-1dc02ff655a3" />

<img width="1175" height="658" alt="Referencia visual 2 (Video Rufus Du Sol)" src="https://github.com/user-attachments/assets/4e995f4b-c6d3-4d6d-9c7a-ef2fa97d39da" />

El referente principal para la estética final se basa en la técnica de vertido acrílico fluido y visualizaciones microscópicas de células.

Texturas: Cuerpos continuos y densos que se fusionan al tocarse, sin bordes duros.

Colores: Contrastes fuertes entre negros profundos/cianes y rosas/corales.

Overlay: Ruido blanco o polvo orgánico flotando en el entorno para unificar la pieza.

#### 4. Dos o más bocetos.
#### 5. Mapa de decisiones.

<img width="2816" height="1536" alt="Gemini_Generated_Image_bv8p4gbv8p4gbv8p" src="https://github.com/user-attachments/assets/92979e26-ee62-4ed5-a093-a81dea99bcf2" />

#### 6. Mapa de interpretación.



#### 7. Justificación del algoritmo elegido.

Para el movimiento, se eligió el algoritmo de Flow Field (Campo de Flujo) alimentado por Ruido de Perlin (noise()), combinado con Agentes Autónomos.
El uso de la función random() estándar genera movimientos erráticos y robóticos. El ruido de Perlin, por su naturaleza suave y progresiva, permite simular con precisión fuerzas físicas reales como corrientes de agua o túneles de viento. Los agentes (partículas) "leen" los ángulos de este campo invisible para decidir su trayectoria, lo que garantiza el flujo hipnótico y organizado característico de la pieza

#### 8. Explicación de la relación audio-visual.

El núcleo audio-visual reside en la función p5.FFT. El código aísla las frecuencias bajas (bass) y utiliza esos valores numéricos para alterar la física de los agentes en tiempo real:

El Umbral de Respiración: Para que la pieza reaccione con precisión y no vibre por el ruido de fondo, se aplicó un "clamp" al mapeo del bajo (map(bassAmount, 120, 255, 5, 255, true)). Si el bajo no supera el nivel 120, la opacidad cae a casi cero. Esto logra que las células se apaguen en los silencios y destellen violentamente con cada golpe (kick).

Aceleración de Turbulencia: El volumen del bajo también se suma al eje Z del ruido de Perlin (zoff), haciendo que las corrientes muten de dirección más rápido en los momentos más intensos de la canción.

#### 9. Evidencia del uso de IA.

La IA actuó como un copiloto de programación (Pair-Programming) y consultoría técnica. Se utilizó para:

Refactorizar el código inicial hacia una arquitectura Orientada a Objetos (Clases FlowField y Particle).

Diagnosticar problemas de servidor local (Error 404) originados por rutas de archivos no relativas en Visual Studio Code.

Traducir conceptos abstractos (ej. "quiero que se vea más orgánico") a funciones matemáticas de p5.js, como la implementación de arreglos de memoria (this.history) y formas complejas (beginShape).

Ajustar principios de diseño editorial en la pantalla de inicio mediante jerarquías tipográficas y funciones trigonométricas para animación.

#### 10. Código fuente.

```c
let audio;
let fft;
let audioStarted = false;
let isLoading = true;
let particles = [];
let flowfield;
let spacing = 20; 
let cols, rows;
let firstFrame = false;
let speedMultiplier = 1.0; 
let darkPalette = ['#121b1e', '#2a4445', '#58bda2', '#212121', '#0a0a0a'];
let pastelPalette = ['#f1948a', '#ffdfba', '#e8e8df', '#baffc9', '#bae1ff'];
let stateAmt = 0; 
let targetStateAmt = 0; 
let climaxTime = 362; 
let climaxTriggered = false; 

function preload() {
  soundFormats("mp3", "ogg");
  audio = loadSound("Innerbloom.mp3.mp3", soundLoaded);
}

function setup() {
  createCanvas(1280, 720); 
  frameRate(60);
  background(10);

  fft = new p5.FFT(0.8, 64);
  
  initializeFlowField();
  for (let i = 0; i < 500; i++) {
    particles.push(new Particle());
  }
}

function soundLoaded() {
  isLoading = false;
  console.log("Audio cargado exitosamente.");
}

function draw() {
  if (isLoading) {
    background(10);
    textAlign(CENTER, CENTER);
    textSize(48);
    fill(127, 222, 197);
    text("CARGANDO AUDIO...", width / 2, height / 2);
    return;
  }

  if (!audioStarted) {
    initialText();
    return;
  }

  if (!firstFrame) {
    background(10);
    firstFrame = true;
  }


  background(10);

  fft.analyze();
  let bass = fft.getEnergy("bass");
  stateAmt = lerp(stateAmt, targetStateAmt, 0.02);

  if (audio.currentTime() >= climaxTime && !climaxTriggered) {
    targetStateAmt = 1;
    speedMultiplier = 3.0; 

    for (let i = 0; i < particles.length; i++) {
      let explosionForce = p5.Vector.random2D().mult(random(15, 30));
      particles[i].applyForce(explosionForce);
      particles[i].history = []; 
    }
    
    climaxTriggered = true; 
    console.log("¡DROP ACTIVADO!");
  }

  flowfield.update(bass);
  for (let i = 0; i < particles.length; i++) {
    let p = particles[i];
    p.follow(flowfield);
    p.interact(); 
    p.update(bass);
    p.edges();
    p.display(bass);
  }
  stroke(255, 255, 255, 30); 
  strokeWeight(1.0);
  for (let i = 0; i < 50; i++) { 
    point(random(width), random(height));
  }
}

function initialText() {
  background(8, 12, 14);
  textAlign(CENTER, CENTER);

  let initHeight = height * 0.35; 
  let interline = 55;

  let c1 = color(88, 110, 110);  
  let c2 = color(127, 222, 197); 
  let c3 = color(241, 148, 138); 

  textFont('Georgia'); 
  textStyle(NORMAL);

  textSize(30);
  fill(c1);
  text("Nueve minutos de simbiosis sonora,", width / 2, initHeight - interline);

  textSize(36); 
  fill(c2);
  text("donde la materia oscura respira y muta,", width / 2, initHeight);

  textSize(42); 
  fill(c3);
  text("hasta florecer en un latido de color.", width / 2, initHeight + interline);

  let controlY = height * 0.75; 
  
  textFont('Courier New');
  textSize(15);
  fill(180);
  
  text("— CONTROLES DEL INSTRUMENTO —", width / 2, controlY - 30);
  text("[1] Modo Oscuro  |  [2] Células Pastel  |  [F] Pantalla Completa", width / 2, controlY);
  text("[↑ / ↓] Velocidad de Corriente  |  [Mouse Drag] Perturbar", width / 2, controlY + 30);
  textFont('Helvetica');
  textSize(28);
  textStyle(BOLD);

  let pulso = sin(millis() / 400.0); 
  let alphaPulso = map(pulso, -1, 1, 80, 255);
  let flotacionY = map(pulso, -1, 1, -5, 5);

  fill(255, 255, 255, alphaPulso * 0.15);
  text("Haz clic para sumergirte", width / 2, (height * 0.92) + flotacionY + 2);

  fill(255, 255, 255, alphaPulso);
  text("Haz clic para sumergirte", width / 2, (height * 0.92) + flotacionY);
  textStyle(NORMAL); 
  textFont('Helvetica');
}

function mousePressed() {
  if (!isLoading && !audioStarted) {
    audio.play(); 
    fft.setInput(audio);
    audioStarted = true;
    noCursor();
    let fs = fullscreen();
    fullscreen(true);
  }
}

function keyPressed() {
  if (key === "1") { targetStateAmt = 0; }
  if (key === "2") { targetStateAmt = 1; }
  if (key === "f" || key === "F") {
    let fs = fullscreen();
    fullscreen(!fs);
  }
  if (keyCode === UP_ARROW) {
    speedMultiplier += 0.2;
  } else if (keyCode === DOWN_ARROW) {
    speedMultiplier = max(0.2, speedMultiplier - 0.2); 
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
  initializeFlowField();
  background(10);
}

function initializeFlowField() {
  cols = floor(width / spacing);
  rows = floor(height / spacing);
  flowfield = new FlowField(spacing);
}

class FlowField {
  constructor(spacing) {
    this.spacing = spacing;
    this.cols = floor(width / spacing);
    this.rows = floor(height / spacing);
    this.field = new Array(this.cols * this.rows);
    this.zoff = 0;
  }

  update(bassAmount) {
    let zIncrement = map(bassAmount, 0, 255, 0.001, 0.03);
    this.zoff += zIncrement;

    let yoff = 0;
    for (let y = 0; y < this.rows; y++) {
      let xoff = 0;
      for (let x = 0; x < this.cols; x++) {
        let index = x + y * this.cols;
        let angle = noise(xoff, yoff, this.zoff) * TWO_PI * 4;
        let v = p5.Vector.fromAngle(angle);
        v.setMag(1); 
        this.field[index] = v;
        xoff += 0.1;
      }
      yoff += 0.1;
    }
  }

  lookup(pos) {
    let column = floor(constrain(pos.x / this.spacing, 0, this.cols - 1));
    let row = floor(constrain(pos.y / this.spacing, 0, this.rows - 1));
    let index = column + row * this.cols;
    if (this.field[index]) {
      return this.field[index].copy();
    } else {
      return createVector(0, 0);
    }
  }
}

class Particle {
  constructor() {
    this.pos = createVector(random(width), random(height));
    this.vel = createVector(0, 0);
    this.acc = createVector(0, 0);
    this.baseMaxSpeed = random(1.5, 3);
    this.colorIndex = floor(random(5));
    this.history = []; 
    this.maxHistory = floor(random(10, 35)); 
  }

  follow(flowfield) {
    let force = flowfield.lookup(this.pos);
    this.applyForce(force);
  }

  interact() {
    if (mouseIsPressed) {
      let mouse = createVector(mouseX, mouseY);
      let d = p5.Vector.dist(this.pos, mouse);
      
      if (d < 150) {
         let force = p5.Vector.sub(this.pos, mouse);
         force.rotate(HALF_PI); 
         force.setMag(map(d, 0, 150, 3, 0));
         this.applyForce(force);
      }
    }
  }

  applyForce(force) {
    this.acc.add(force);
  }

  update(bassAmount) {
    this.vel.add(this.acc);
    let currentMaxSpeed = (this.baseMaxSpeed + map(bassAmount, 0, 255, 0, 3.5)) * speedMultiplier;
    this.vel.limit(currentMaxSpeed);
    this.pos.add(this.vel);
    this.acc.mult(0);
    this.history.push(createVector(this.pos.x, this.pos.y));

    if (this.history.length > this.maxHistory) {
      this.history.splice(0, 1);
    }
  }

  display(bassAmount) {
    let cDark = color(darkPalette[this.colorIndex]);
    let cPastel = color(pastelPalette[this.colorIndex]);
    let finalColor = lerpColor(cDark, cPastel, stateAmt);
    let currentAlpha = map(bassAmount, 120, 255, 5, 255, true);
    finalColor.setAlpha(currentAlpha);
    
    fill(finalColor);
    noStroke(); 
    
    beginShape();
    for (let i = 0; i < this.history.length; i++) {
      let pos = this.history[i];
      let dynamicWidth = sin(i * 0.2) * 2; 
      vertex(pos.x + dynamicWidth, pos.y);
    }
    endShape();
    this.drawDetails(finalColor, currentAlpha);
  }

  drawDetails(baseColor, currentAlpha) {
    let detailColor = color(hue(baseColor), saturation(baseColor), brightness(baseColor));
    detailColor.setAlpha(currentAlpha * 0.6);
    stroke(detailColor);
    noFill();
    strokeWeight(1.5); 

    for (let i = 0; i < this.history.length; i++) {
      let pos = this.history[i];
      if(random(1) < 0.25) { 
        point(pos.x + random(-3, 3), pos.y + random(-3, 3));
      }
    }
  }

  edges() {
    let hitEdge = false;

    if (this.pos.x > width) { this.pos.x = 0; hitEdge = true; }
    if (this.pos.x < 0) { this.pos.x = width; hitEdge = true; }
    if (this.pos.y > height) { this.pos.y = 0; hitEdge = true; }
    if (this.pos.y < 0) { this.pos.y = height; hitEdge = true; }

    if (hitEdge) {
      this.history = [];
    }
  }
}
````

#### 11. Enlace al sketch.

No lo tengo ya que lo elabore en Visual, por que en P5.js no podia subir la melodia por el tamaño del archivo.

#### 12. Capturas o registros de momentos importantes de la pieza.

<img width="1910" height="850" alt="Momento 1 " src="https://github.com/user-attachments/assets/9525e195-faa6-4fa4-8d1c-22ecd19bdc0d" />

<img width="1908" height="852" alt="image" src="https://github.com/user-attachments/assets/9ce57375-e0f1-4bf0-86ec-cd676745b601" />

<img width="1913" height="852" alt="image" src="https://github.com/user-attachments/assets/9e9bc5c5-c17e-4e8d-93eb-b7c901752567" />




## Bitácora de reflexión
