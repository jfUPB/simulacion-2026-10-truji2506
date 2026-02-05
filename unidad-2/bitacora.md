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

#### Solución

#### Actividad 6

#### Enunciado

#### Solución

#### Actividad 7

#### Enunciado

#### Solución

#### Actividad 8

#### Enunciado

#### Solución
## Bitácora de aplicación 



## Bitácora de reflexión


