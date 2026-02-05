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

```
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

#### Solución

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

