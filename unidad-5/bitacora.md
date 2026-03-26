# Unidad 5
## Bitácora de proceso de aprendizaje

#### Acividad 1

#### Enunciado

📤 Bitácora

Capa de comportamiento:

¿Qué propiedades tiene cada partícula? Clasifícalas: ¿Cuáles definen su estado físico? ¿Cuáles su estado vital?
¿Qué condición determina que una partícula “muere”? ¿Es una muerte instantánea o gradual?
¿Cómo se actualiza la partícula en cada frame? Identifica el patrón motion 101 dentro de la partícula.
Capa de estructura:

¿Quién crea las partículas? ¿En qué momento?
¿Quién decide cuándo eliminar una partícula del array?
¿Por qué se recorre el array en orden inverso para eliminar? ¿Qué pasaría si no se hiciera así?
Si no eliminaras nunca las partículas, ¿Qué pasaría con la memoria y el rendimiento? Haz el experimento: comenta la línea que elimina y observa el frame rate.
Capa de visualización:

¿Qué elementos visuales usa para representar una partícula?
¿Cómo se conecta el “tiempo de vida” con la apariencia visual?
Si quisieras cambiar la representación visual (por ejemplo, usar líneas en vez de círculos), ¿Qué cambiarías y qué NO cambiarías?

##  Solución

1. Su estado físico: Imagina que la partícula es un carrito. Tiene una ubicación actual (position), una velocidad a la que se mueve (velocity), y un motor o empuje (acceleration).

Su estado vital: Tiene una especie de "barra de salud" o energía vital (lifespan) que empieza llena (en 255).

2. Muere cuando su "barra de salud" (lifespan) cae por debajo de cero. Es una muerte gradual, porque no desaparece de un plumazo; en cada instante (cada frame), su salud disminuye un poquito (le restan 2 puntos). Se va apagando poco a poco.

3. Es como manejar: el empuje o aceleración altera la velocidad a la que vas, y esa velocidad cambia tu posición en el mapa. Al final del paso, el empuje vuelve a cero para estar listo para recibir una nueva fuerza (como soltar el acelerador).

4. El programa principal (el jefe, que está en sketch.js) crea una partícula nueva todo el tiempo, constantemente, unas 60 veces por segundo en la función draw(). Las va metiendo en una lista (el array particles).

5. Ese mismo programa principal. Revisa su lista, le pregunta a cada partícula "¿ya te quedaste sin energía?" (isDead()), y si la respuesta es sí, la saca de la lista y la desecha (splice).

6. Imagínate una fila de personas con turnos asignados (1, 2, 3, 4...). Si estás revisando desde el principio y sacas al número 2 de la fila, el que era el número 3 da un paso al frente y se convierte en el nuevo número 2. Como tú ya vas a revisar el turno 3, ¡te saltaste a esa persona! Si revisas la fila de atrás hacia adelante, sacar a alguien no mueve a los que aún no has revisado.

7. Tendrías un problema de "acumulación de basura". El programa seguiría calculando la posición y la matemática de miles de partículas "fantasmas" que ya ni se ven. La memoria del computador se llenaría, el programa se pondría lentísimo (bajan los FPS) y eventualmente colapsaría.

8. Usa formas geométricas súper básicas: dibuja un círculo (circle), le pone un color de relleno (fill) y un borde o contorno (stroke).

9. Esa "barra de salud" (lifespan) de la que hablamos antes está conectada directamente a la transparencia (el canal alfa) del color. Por eso, a medida que la partícula pierde salud, se vuelve cada vez más transparente hasta que se desvanece por completo como un fantasma.

10. Lo único que cambiarías sería el método show() (el vestuario). Ahí borrarías la palabra circle y pondrías line.

Lo que NO cambiarías en absoluto es todo lo demás: la física y la forma de restar vida (el Comportamiento) seguirían igual, y el jefe creando y eliminando listas (la Estructura) ni se enteraría de que ahora las partículas se ven distintas.

#### Acividad 2

#### Enunciado

Comparación con Example 4.2:

¿Qué responsabilidades que antes estaban en draw() ahora están dentro de la clase Emitter?
¿Cuál es la ventaja de encapsular la lógica de emisión en una clase separada?
En este ejemplo hay un array de emitters. ¿Quién crea los emitters? ¿Quién crea las partículas dentro de cada emitter?
Dibuja un diagrama que muestre la jerarquía: sketch → [emitters] → [partículas]. ¿Cuántos niveles de “colección” hay?
Transferencia conceptual:

Describe este ejemplo usando palabras que NO mencionen p5.js, JavaScript, ni ninguna herramienta específica. Usa solo términos como: entidad, estado, colección, emisor, ciclo de vida, fuerza.

##  Solución

1. Imagina que antes el programa principal (draw()) era un gerente que intentaba hacer todo él solo: tenía la lista de empleados (el array particles), contrataba a los nuevos (push) y despedía a los que se quedaban sin energía (el ciclo for inverso). Ahora, el gerente contrató a un "Jefe de Departamento" llamado Emitter. Este nuevo jefe se llevó la carpeta con la lista de empleados (this.particles = []), la tarea de contratar (addParticle()) y la de supervisar y despedir (run()).

2. Delegación y orden. Si el gerente principal (sketch.js) quiere abrir 5 fábricas distintas en diferentes lugares de la pantalla, no tiene que micro-gestionar a miles de empleados individualmente. Solo tiene que contratar a 5 jefes (Emitters) y decirles "hagan su trabajo". El código principal queda súper limpio y fácil de leer.

3. Al Emitter (el jefe de fábrica) lo crea el programa principal (sketch.js), por ejemplo, cada vez que el usuario hace clic con el mouse (mousePressed).

A las partículas (los empleados) las crea su respectivo Emitter internamente, usando su función addParticle().

4. <img width="2816" height="1536" alt="Gemini_Generated_Image_eld3a7eld3a7eld3" src="https://github.com/user-attachments/assets/f2e1ea87-cd2d-4fc6-a078-749ca3665436" />

Hay dos niveles de colección (como carpetas dentro de otras carpetas). El primer nivel es la lista de emisores que tiene el programa principal. El segundo nivel es la lista de partículas que tiene cada emisor por dentro.

5. El sistema opera mediante un emisor que actúa como administrador de una colección local. Este emisor se encarga de instanciar cada entidad y someterla a una fuerza inicial. De manera independiente, cada entidad gestiona su propio estado interno mientras avanza su ciclo de vida. Cuando este ciclo llega a su fin, el emisor detecta el cambio de estado y retira a la entidad de la colección para optimizar el ecosistema.


#### Acividad 3

#### Enunciado

##  Solución

#### Acividad 4

#### Enunciado

##  Solución


## Bitácora de aplicación 

#### Acividad 5

#### Enunciado

##  Solución

## Bitácora de reflexión

#### Acividad 6

#### Enunciado

##  Solución
