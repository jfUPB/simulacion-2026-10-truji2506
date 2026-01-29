# Unidad 1

## Bitácora de proceso de aprendizaje

#### Actividad 1 

#### Enunciado:

Piensa y describe en una sola frase y en tus propias palabras cómo la aleatoriedad influye en el arte generativo.]

#### Respuesta:

La aleatoriedad es el momento de la vida que transforma un sistema rigido de código en un organismo digital capaz de volverlo "Organico", hablando desde la exploración.

#### Actividad 2 

#### Enunciado:

Analicemos juntos el código del ejemplo Example 0.1: A Traditional Random Walk del texto guía.

Realiza el siguiente experimento y reporta los resultados en tu bitácora:

Modifica el código del ejemplo Example 0.1: A Traditional Random Walk.
Antes de ejecutar el código, escribe en tu bitácora qué esperas que suceda.
Ejecuta el código y escribe en tu bitácora qué sucedió realmente.
Ocurrió lo que esperabas? ¿Por qué crees que sí o por qué crees que no?

#### Respuesta:

1. La modificación del código fue en la clase Walker, en el show modifiqué para que se viera en vez de un punto moviendose aleatoriamente que fuera un circulo con tamaño de 20.
2. Se va a ver en vez de un punto, un circulo moviendose aleatoriamente, ademas de que se le agrego un tamaño mas grande para que fuera dibujando en el lienzo, tambien jugue con el movimento que tomara varias direcciones
3. Ejecutando el codigo, sucedio lo esperado hubo el cambio de figura a renderizar con su respectivo tamaño, y se mueve totalmente random
4. Si, ocurrio lo que esperaba.

#### Actividad 3

#### Enunciado:

En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.
Modifica el código de la caminata aleatoria para que utilice una distribución no uniforme, favoreciendo el movimiento hacia la derecha.

#### Respuesta:

1. Distribución uniforme es cuando se utiliza la función random y esto hace que por ejemplo de un random(0, 100) todos los números tengan las mismas posibilidades de que ocurran.
   Distribución no uniforme es cuando se utiliza la función randomGaussian y esto hace que las probabilidades esten sesgadas y no todos los eventos tengan las mismas probabilidades de ocurrir.
2. 
Código modificado

```
let walker;

function setup() {
  createCanvas(640, 240);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0, 50);
    point(this.x, this.y);
  }

  step() {
    let stepX = randomGaussian(0, 1);
    let stepY = randomGaussian(0, 1);

    this.x += stepX;
    this.y += stepY;
  }
}
```

Lo que se evidenció

<img width="638" height="266" alt="Evidencia actividad 3" src="https://github.com/user-attachments/assets/47f20112-2fc1-4412-b2ce-36c384894bff" />

#### Actividad 4

#### Enunciado:

Una vez has entendido el concepto de distribución normal, vas a pensar en una nueva manera de visualizarlo.

Crea un nuevo sketch en p5.js que represente una distribución normal.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.

#### Respuesta:

```
let color;

function setup() {
  createCanvas(640, 240);
  background(520);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 80);
  let y = randomGaussian(240, 80);
  
  noStroke();
  fill(0, 20);
  circle(x, y, 80);
}
```
Enlace 

https://editor.p5js.org/truji2506/sketches/1HDKR_8eW

Captura de pantalla 

<img width="636" height="241" alt="Evidencia actividad 4 " src="https://github.com/user-attachments/assets/c2ab66a1-a39a-4a70-bfec-40fb1f710d16" />

#### Actividad 5

#### Enunciado:

Ahora vas a:

Crea un nuevo sketch en p5.js donde modifiques uno de los ejemplos anteriores y adiciones de Lévy flight.
Explica por qué usaste esta técnica y qué resultados esperabas obtener.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora.

## Bitácora de aplicación 

#### Actividad 7:

#### Enunciado:

Reporta en tu bitácora lo siguiente:

Un texto donde expliques el concepto de obra generativa.
Copia el código en tu bitácora.
Coloca en enlace a tu sketch en p5.js en tu bitácora.
Selecciona una captura de pantalla de tu sketch y colócala en tu bitácora

#### Respuesta:

1. A través de un sistema autónomo, la pieza busca imitar el comportamiento de partículas naturales —como una mota de polvo en la luz o un organismo unicelular— que se desplazan sin un rumbo fijo, pero bajo leyes físicas invisibles.

2. 
```
let x, y;
let prevX, prevY;

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(10); // Fondo oscuro tipo "espacio"
  x = width / 2;
  y = height / 2;
  prevX = x;
  prevY = y;
}

function draw() {
  // 1. LÉVY FLIGHT (El concepto del salto)
  // Usamos un número uniforme para decidir si damos un "gran salto"
  let stepSize;
  let r = random(1); 
  
  if (r < 0.02) { 
    // 2% de probabilidad de dar un paso gigante (Lévy Flight)
    stepSize = random(50, 100); 
  } else {
    // 98% de probabilidad de dar un paso normal
    // 2. DISTRIBUCIÓN NORMAL (Para pasos pequeños y orgánicos)
    stepSize = randomGaussian(2, 5); 
  }

  // 3. RANDOM() (Para la dirección)
  // Elegimos un ángulo aleatorio uniforme en 360 grados
  let angle = random(TWO_PI);
  
  let nextX = x + cos(angle) * stepSize;
  let nextY = y + sin(angle) * stepSize;

  // Dibujamos la línea del camino
  strokeWeight(2);
  // Color aleatorio neón (Distribución uniforme)
  stroke(random(100, 255), random(255), 255, 150); 
  line(x, y, nextX, nextY);

  // Actualizamos la posición actual
  x = nextX;
  y = nextY;
}

function mousePressed() {
  background(10); // Limpiar con click
  x = width / 2;
  y = height / 2;
}
```

3.

https://editor.p5js.org/truji2506/sketches/u3aOI2Gtz

4.

<img width="916" height="779" alt="image" src="https://github.com/user-attachments/assets/013e971e-653d-4ca3-9870-4ea2c8dfdad1" />



## Bitácora de reflexión




