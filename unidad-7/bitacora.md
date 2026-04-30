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


## Bitácora de reflexión
