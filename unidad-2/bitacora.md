# Unidad 2

## Bitácora de proceso de aprendizaje

#### Actividad 1

#### Enunciado

Distruta esta actividad como quieras. Busca inspiración. Te deseo que te enamores del tema, es irresistible. Te pediré que me cuentes qué trabajo te gustó más y por qué.

#### Solución

En lo personal, esta fue la obra que mas me gusto, 

<img width="1841" height="846" alt="image" src="https://github.com/user-attachments/assets/d4161e19-ee43-4a58-9a68-33a35eacfd55" />

Ya que con un codigo simple se realizó una obra muy llamativa e interactiva

#### Actividad 2

#### Enunciado

¿Cómo funciona la suma dos vectores en p5.js?
¿Por qué esta línea position = position + velocity; no funciona?

#### Solución

1. La suma de vectores se realiza con el metodo .add(), cuando se ejecuta position.add(velocity), suma los componentes individuales
2. Porque serian 3 reglas que irian en contra del lenguaje de JavaScript, position y velocity no son valores simples, estos son objetos que puede contener multiples propiedades

#### Actividad 3

#### Enunciado

¿Qué tuviste que hacer para hacer la conversión propuesta?
Escribe el código que utilizaste para resolver el ejercicio.

#### Solución

1. Se modifico un codigo de la unidad 1 añadiendole vectores

```ruby
// The Nature of Code
// Walker con p5.Vector (Estructura original)

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
    // Sustituimos this.x y this.y por un solo vector
    this.pos = createVector(width / 2, height / 2);
  }

  show() {
    stroke(0);
    // Accedemos a los componentes mediante el punto
    point(this.pos.x, this.pos.y);
  }

  step() {
    const choice = floor(random(4));
    
    // Aplicamos los cambios directamente a las propiedades x o y del vector
    if (choice == 0) {
      this.pos.x++;
    } else if (choice == 1) {
      this.pos.x--;
    } else if (choice == 2) {
      this.pos.y++;
    } else {
      this.pos.y--;
    }
  }
}
```

#### Actividad 4

#### Enunciado

¿Qué resultado esperas obtener en el programa anterior?
¿Qué resultado obtuviste?
Recuerda los conceptos de paso por valor y paso por referencia en programación.
¿Qué tipo de paso se está realizando en el código?
¿Qué aprendiste?

#### Solución

1. Esperaba obtener que en el primer console.log muestre el vector original (6,9) y que el segundo mostrala lo mismo, asumiento que el función playingVector trabaja con una copia local y que no afectaba la variable global
2. El resultado que obtuve

<img width="319" height="70" alt="image" src="https://github.com/user-attachments/assets/edfe8e68-1a8c-464d-9a97-e1926edc703e" />

El valor de la variable original cambio

3. Se está realizando un paso por referencia

   Paso por valor y paso por referencia

   En el codigo le estoy dando la apertura de la caja donde esta guardado el vector, entonces cuando la funcion modifica v.x y v.y esta alterando el contenido de la caja original.

4. Aprendi que los vectores son objetos. que tengo que tener cuidado cuando los vectores reciben un parametro y este lo altera permanentemente al vector original.

#### Actividad 5

#### Enunciado

¿Para qué sirve el método mag()? Nota que hay otro método llamado magSq(). ¿Cuál es la diferencia entre ambos? ¿Cuál es más eficiente?
¿Para qué sirve el método normalize()?
Te encuentras con un periodista en la calle y te pregunta ¿Para qué sirve el método dot()? ¿Qué le responderías en un frase?
El método dot() tiene una versión estática y una de instancia. ¿Cuál es la diferencia entre ambas?
Ahora el mismo periodista curioso de antes te pregunta si le puedes dar una intuición geométrica acerca del producto cruz. Entonces te pregunta ¿Cuál es la interpretación geométrica del producto cruz de dos vectores? Tu respuesta debe incluir qué pasa con la orientación y la magnitud del vector resultante.
¿Para que te puede servir el método dist()?
¿Para qué sirven los métodos normalize() y limit()?

#### Solución

1. Mag() calcula la longitud  real del vector usando la raiz cudrada de x, y eso al cuadrado y MagSq() calcula la magnitud al cuadrado y este evita la raiz
2. normalize() sirve para convertir un vector en un vector unitario, es decir, hace que su longitud sea exactamente 1 sin cambiar la dirección hacia la que apunta.
3. Que es una herramienta que nos dice qué tanto apunta un vector en la misma dirección que otro; si el resultado es alto, van de la mano; si es cero, son perpendiculares
4. De instancia (v.dot(w)): Modifica o actúa sobre el objeto específico v.

Estática (p5.Vector.dot(v, w)): Es una función de utilidad de la "fábrica" de vectores que toma dos vectores y da el resultado sin necesidad de que uno pertenezca al otro.

5. El producto cruz genera un nuevo vector que es totalmente perpendicular al plano formado por los dos originales (su orientación); su magnitud representa el área del paralelogramo que ambos vectores dibujarían en el espacio
6. Sirve para calcular la distancia euclidiana entre dos puntos (tratados como vectores de posición). Es como tirar una regla invisible entre el vector A y el vector B.
7. normalize(): Fija la fuerza (magnitud) en 1. Útil para obtener solo la dirección.

limit(): Restringe la magnitud de un vector a un valor máximo. Si el vector es más corto, se queda igual; si es más largo, lo "recorta" a ese máximo. Es fundamental para controlar velocidades máximas en simulaciones.

#### Actividad 6

#### Enunciado

El código que genera el resultado que te pedí.
¿Cómo funciona lerp() y lerpColor().
¿Cómo se dibuja una flecha usando drawArrow()?


#### Solución
1.
```ruby
function setup() {
    createCanvas(400, 400);
}

function draw() {
    background(200);

    let v0 = createVector(50, 50);   // Origen común
    let v1 = createVector(300, 0);  // Vector rojo
    let v2 = createVector(0, 300);  // Vector azul
    
    // El vector verde conecta la punta de v1 con la punta de v2
    // Matemáticamente es: v2 - v1
    let v_green = p5.Vector.sub(v2, v1);
    
    // Animación de interpolación (0 a 1)
    let amt = map(sin(frameCount * 0.03), -1, 1, 0, 1);
    
    // El vector morado nace en v0 y se mueve a lo largo del verde
    // Interpolamos entre el vector v1 y el v2
    let v3 = p5.Vector.lerp(v1, v2, amt);

    // 1. Dibujamos los vectores principales desde el origen (v0)
    drawArrow(v0, v1, 'red');
    drawArrow(v0, v2, 'blue');
    drawArrow(v0, v3, 'purple');

    // 2. Dibujamos el vector verde EMPEZANDO en la punta del rojo (v0 + v1)
    let puntaRoja = p5.Vector.add(v0, v1);
    drawArrow(puntaRoja, v_green, 'green');
}

function drawArrow(base, vec, myColor) {
    push();
    stroke(myColor);
    strokeWeight(3);
    fill(myColor);
    translate(base.x, base.y);
    line(0, 0, vec.x, vec.y);
    rotate(vec.heading());
    let arrowSize = 7;
    translate(vec.mag() - arrowSize, 0);
    triangle(0, arrowSize / 2, 0, -arrowSize / 2, arrowSize, 0);
    pop();
}
```
2. Ambas funciones realizan una interpolación lineal, que consiste en encontrar un valor intermedio entre dos puntos basándose en un porcentaje (un número entre 0 y 1).

lerp(valor1, valor2, amt): Calcula un número entre dos números. Si amt es 0.5, devuelve el punto medio exacto. En vectores, p5.Vector.lerp(v1, v2, amt) calcula un nuevo vector que está en el camino entre v1 y v2.

lerpColor(c1, c2, amt): Mezcla dos colores. Si tienes rojo y azul con un amt de 0.5, el resultado será un color morado. Es muy útil para transiciones suaves de color en animaciones.

3. La función drawArrow() no es nativa de p5.js, es una función personalizada que utiliza transformaciones de coordenadas para facilitar el dibujo. Funciona así:

translate(base.x, base.y): Mueve el "punto 0,0" del lienzo a la ubicación donde debe nacer la flecha.

line(0, 0, vec.x, vec.y): Dibuja el cuerpo de la flecha desde el nuevo origen hasta la punta definida por el vector.

rotate(vec.heading()): Gira todo el sistema de dibujo para que el eje X apunte exactamente en la dirección del vector.

Dibujo del triángulo:

Se traslada el origen al final del vector (vec.mag()).

Se dibuja un triangle() que, gracias a la rotación previa, siempre queda alineado con la punta de la línea.

push() y pop(): Aseguran que estas traslaciones y rotaciones no afecten a los demás elementos que se dibujen después.


#### Actividad 7

#### Enunciado

Cuál es el concepto del marco motion 101 y cómo se interpreta geométricamente.
¿Cómo se aplica motion 101 en el ejemplo?

#### Solución

#### Actividad 8

#### Enunciado

¿Qué observaste cuando usas cada una de las aceleraciones propuestas?

#### Solución



## Bitácora de aplicación 



## Bitácora de reflexión





