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

```ruby
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

```ruby
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

1. A través de un sistema autónomo, la pieza busca imitar el comportamiento de partículas naturales como una mota de polvo en la luz o un organismo unicelular que se desplazan sin un rumbo fijo, pero bajo leyes físicas invisibles.

La idea de esta obra generativa siempre te va a brindar una posibilidad de diseño para dibujar, teniendo en cuenta que siempre va a ser aleatorio puede imaginarte dependiendo de lo que te vaya mostrando imaginarte que puedas dibujar. 

En esta obra de arte generativa aplique los siguientes conceptos,

Random()
RandomGaussian()
Levy Flight()

La funcion random() fue aplicado en la dirección de la obra, donde se calcula alguna posición 360 grados y por ender se utilizó el TWO_PI

La función RandomGaussian() Fue aplicado para darle un poco mas de manejo a las decisiones que puede tomar la obra, y no sea aleatorio

La función Levy Fligh() fue aplicado para darle la probabilidad de dar un paso "Grande" en el walkdraw donde se le da el 2% de la posibilidad de pase y el 98% ingrese al randomgaussian().

2. 
```ruby
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

#### Actividad 8
```
let x, y;
```
Variables que almacenan la posición actual
```
let prevX, prevY;
```
Dibujar lineas en lugar de puntos sueltos
```
createCanvas(windowWidth, windowHeight);
```
Valores automaticos para detectar el hancho y largo de la pantalla y asi tener las condiciones el lienzo 
```
background(10);
```
Color del fondo
```
x = width / 2;
y = height / 2;
```
Posición inicial
```
prevX = x;
prevY = y;
```
Esto evita una linea desde las coordenadas (0,0) hasta el centro en el primer milisegundo 
```
let stepSize;
```
Declaro una variable vacia, y en las siguientes lineas ya se le dará un valor
```
let r = random(1); 
```
Aqui se aplica la distribución uniforme, genera un numero decimal del 0 al 1 
```
if (r < 0.02) { 
```
Yo lo veo como muchos pasos y cada vez que un numero es menor a 0.02 dar un paso grande que solo pasa el 2% de las veces 
```
stepSize = random(50, 100); 
```
Y si entramos en este if se convierte en un paso grande de 50, a 100 pixeles
```
 stepSize = randomGaussian(2, 5);
```
Y ya el 98% del tiempo nos entramos en el else, donde la mayoria de pasos seran de 2 pixeles con una desviación estandar de 5 y esto genera un comulo de rayitas esperando a dar el paso grande 
```
let angle = random(TWO_PI);
```
El two_pi equivale a 360 grados, y al usar el random le digo a P5 que escoja entre 0 y 6.25 radianes
```
let nextX = x + cos(angle) * stepSize;
```
el cos siempre te dice cuando se mueve algo en el eje x y devuelve un valor de -1 y 1, en el stepsize multiplicamos ese valor por la longitud del paso y lo sumamos a la posición actual para obtener la posición del destino
```
let nextY = y + sin(angle) * stepSize;
```
Al igual que el cos pero se mueve en el Y
```
strokeWeight(2);
```
Define el grosor de la linea
```
stroke(random(100, 255), random(255), 255, 150);
```
Distribución uniforme, donde los colores son totalmente randoms junto con su alpha 
```
line(x, y, nextX, nextY);
```
Las coordenadas x,y son el punto de partida 
los next, es el punto del destino, que son los que acabamos de calcular con el paso de levy 
```
  x = nextX;
  y = nextY;
```
Como yo lo veo es como decirle olvida donde antes estabas y esta es tu nueva posición para el proximo frame
```
function mousePressed() {
  background(10); // Limpiar con click
  x = width / 2;
  y = height / 2;
```
#### Enunciado 

En tu bitácora de aprendizaje. Responde con tus propias palabras a las siguientes preguntas.

Describe la diferencia fundamental entre la aleatoriedad generada por random() y la apariencia de aleatoriedad del Ruido Perlin (noise()). ¿En qué tipo de situación usarías cada una?
Explica con tus palabras qué es una distribución de probabilidad. ¿Qué diferencia visual produce una caminata aleatoria con una distribución uniforme versus una con una distribución normal?
¿Cuál es el papel de la aleatoriedad en el arte generativo? Menciona al menos dos funciones distintas que cumple
Piensa en tu obra final (Actividad 07). Describe uno de los conceptos de aleatoriedad que usaste y explica por qué fue una elección adecuada para lograr el efecto que buscabas.
¿Qué es un “paseo” o “caminata” (walk) en el contexto de la simulación? ¿Qué característica particular tiene una caminata de tipo “Lévy flight”?

#### Respuesta

1. La diferencia en el la función random () y el Ruido Perlin (noise()) 

La función random() es totalmente aleatorio, donde el número que genera no tiene nada que ver con el anterior y esto produce saltos bruscos

A diferencia del random() el Ruido Perlin (Noise()) es mucho mas armonico y dependiente, todos los valores estan conectados creando una transición suave y fluida.

2. La diferencia visual se basa en lo siguiente

Uniforme: El caminante parece un robot confundido, este se mueve en todas las direcciones con la misma fuerza, llenando el espacio de forma muy cuadrada y dispersa.

Normal (Gaussiana): El uso de este concepto tiende a quedare mucho tiempo "Merodeando" cerca de un punto central y rara vez se aleja mucho.

3. Creeria que el papel de la aleatoriedad en el arte generativo se basa mas que todo en la autonomia y sorpresa ademas de una variabilidad infinita, donde permite que la obra tome sus propias decisiones, logrando que el artista se sorprenda con resultados del código que no brinda el dibujo y la variabilidad infinita garantiza que la obra sea unica cada vez que se ejecuta

4. En mi obra use el concepto Levy Flight, donde busque imitar un comportamiento de exploración natural, donde no quise que el movimiento fuera monotono y los saltos largos de vez en cuando permiten que el lienzo no se saturara en un solo lugar, donde esto le dio una estetica mucho mas dinamica y organica a la obra final.

5. Caminata (Walk): Es un proceso donde la posición actual depende de la anterior más un paso al azar

Levy Flight: Su principal caracteristica es que no es propocional, mientras que una caminata normal da pasos de tamaño similar, el levy flight combina muchisimos pasos diminutos con saltos gigantescos de forma imprevista.







