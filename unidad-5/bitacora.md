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

📤 Bitácora

¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?
¿Por qué es importante que el Emitter no necesite saber qué tipo específico de partícula está gestionando? Explica esto con tus propias palabras.
Si mañana quisieras agregar un tercer tipo de partícula, ¿Qué tendrías que crear y qué NO tendrías que modificar?
Compara con Example 4.2: ¿Cambió la lógica del Emitter? ¿Cambió la lógica de muerte? ¿Qué capa del sistema se modificó y cuáles permanecieron intactas?

##  Solución

1. En común: Tanto la partícula normal (el círculo) como el Confetti (el cuadrado) comparten el mismo "motor" y las mismas reglas de vida. Ambas heredan de la clase Particle su forma de moverse (velocidad y aceleración), cómo les afecta la gravedad, y cómo se les va gastando la "barra de salud" (lifespan) hasta morir.

De diferente: Lo único que cambia es su apariencia exterior. La partícula original se dibuja como un círculo simple, mientras que el Confetti sobrescribe esa instrucción (el método show()) para dibujarse como un cuadrado que va girando mientras cae.

2. Imagina que el Emitter es el director de un teatro y las partículas son los actores. El director solo necesita decir la orden "¡Acción!" (llamar al método run()), y cada actor sabe exactamente qué papel le toca interpretar (si debe verse como círculo o como confeti). Si el director tuviera que ir uno por uno diciéndoles "tú eres un círculo, muévete así; tú eres un cuadrado, gira así", se volvería loco. Esta independencia (el polimorfismo) hace que el sistema sea súper eficiente y fácil de manejar.

3. Tendría que crear: Un nuevo archivo con una nueva clase (por ejemplo, class Estrella extends Particle) y escribirle su propio "vestuario" en el método show(). Además, tendrías que ir al Emitter y actualizar la función de "contratación" (addParticle()) para decirle: "ahora tienes un 33% de probabilidad de crear estrellas".

NO tendría que modificar: No tocarías en absoluto la clase padre Particle (el motor base), ni tampoco el ciclo principal del emisor (run()) que las actualiza y elimina. La estructura y la física base quedan intactas.

4. Lógica del Emitter y de Muerte: ¡Siguen siendo exactamente las mismas! El proceso de recorrer la lista hacia atrás y eliminar a los que ya no tienen energía (isDead()) no cambió en nada.

Capas:

La capa de Estructura se modificó solo un poquito (el addParticle ahora tira una moneda al aire para decidir qué tipo de partícula crea).

La capa de Visualización fue la que realmente se amplió al crear la clase Confetti.

La capa de Comportamiento (la física y el ciclo de vida base) permaneció totalmente intacta.

#### Acividad 4

#### Enunciado

📤 Bitácora

Fuerzas globales vs. locales:

En Example 4.6, ¿Dónde se define la gravedad? ¿Quién la aplica a las partículas? ¿Es una fuerza global o local?
En Example 4.7, ¿Qué diferencia hay entre la gravedad y la fuerza del repeller? ¿Dónde “vive” cada una?
La fuerza del repeller depende de la distancia entre la partícula y el repeller. ¿Qué principio físico se está modelando?
¿Cambió la clase Particle entre Example 4.6 y 4.7? ¿Qué implica esto sobre la separación entre comportamiento de la partícula y fuerzas externas?
Tabla comparativa:

Completa la siguiente tabla en tu bitácora:

Aspecto	4.2	4.4	4.5	4.6	4.7
¿Quién crea partículas?					
¿Hay clase Emitter?					
¿Hay herencia?					
¿Hay fuerzas externas?					
¿Hay interacción entre elementos?					
¿Cómo mueren las partículas?					
Modificación quirúrgica:

Elige UNA de estas modificaciones sobre el Example 4.7 e impleméntala:

(a) Cambiar la visualización sin cambiar fuerzas ni estructura.
(b) Cambiar las fuerzas sin cambiar la estructura ni la visualización.
(c) Cambiar la condición de muerte sin cambiar la visualización ni las fuerzas.
Para la modificación que elegiste, responde:

¿Qué líneas de código tocaste?
¿Qué clases/funciones modificaste?
¿Qué partes del programa NO necesitaste modificar?
¿Por qué fue posible hacer este cambio sin afectar las demás capas?

##  Solución

1. La gravedad se define en el archivo principal, el sketch.js (let gravity = createVector(0, 0.1)). Quien se encarga de aplicarla es el jefe de la fábrica, el Emitter, a través de su método applyForce. Es una fuerza global porque es como el clima o el viento en una ciudad: afecta a todos los ciudadanos (partículas) exactamente por igual, sin importar dónde estén parados.

2. La gravedad sigue siendo "el clima" que afecta a todos por igual y vive en el archivo principal (sketch.js). La fuerza del repulsor, en cambio, vive dentro de un objeto específico (la clase Repeller). Es una fuerza local o relativa, porque es como un imán gigante en medio de la calle: su fuerza depende de qué tan cerca o lejos esté cada partícula de ese imán.

3. Se está modelando la atracción gravitacional (como los planetas) o el electromagnetismo (como los imanes). El principio clave es que la fuerza es inversamente proporcional al cuadrado de la distancia. Mientras más cerca estás, el empujón es muchísimo más fuerte; si te alejas un poco, la fuerza cae drásticamente. Por eso divide por distance * distance.

4. ¡No cambió casi nada en su estructura fundamental! A la partícula no le importa si la empuja el viento global o un imán local; ella solo tiene una boca (applyForce) por la que recibe un empujón (un vector) y se lo suma a su motor (acceleration). Esto demuestra una separación perfecta: el comportamiento interno de la partícula es independiente de lo que pase en el mundo exterior.

5. <img width="2816" height="1536" alt="Gemini_Generated_Image_w2o2thw2o2thw2o2" src="https://github.com/user-attachments/assets/c179b157-69f5-4ba4-ab9f-d72dd001e376" />

6. Toqué las instrucciones de dibujo (stroke, fill, circle) y las reemplacé por líneas o formas distintas, y le di un color diferente.

7. Modifiqué únicamente la función show() dentro de la clase Particle (en el archivo particle.js).

8. No toqué el sketch.js (el jefe), ni el emitter.js (el gerente de contratación), ni el repeller.js (el imán). Tampoco toqué la función update() o applyForce() dentro de la misma partícula. La estructura y las físicas quedaron intactas.

9. Porque el código está modularizado (encapsulado). El gerente de la fábrica (el Emitter) solo le dice a la partícula "es tu turno de actuar" (llamando a run()). Al gerente no le importa si la partícula se dibujó como un círculo o como un cuadrado rojizo; la visualización es un problema exclusivo del departamento de "maquillaje" (el método show()).

## Bitácora de aplicación 

#### Acividad 5

#### Enunciado

##  Solución

## Bitácora de reflexión

#### Acividad 6

#### Enunciado

##  Solución
