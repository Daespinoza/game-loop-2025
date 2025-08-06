# Proyecto: [Nombre del videojuego]

**Game Jam 2025**  
**Fecha:** Julio 30 - Agosto 3  
**Tema:** *Loops / Ciclos / Repetición*  
**Hecho en:** Unity 2D (Built-in Render Pipeline)  
**Lenguaje:** C#

---

## Descripción del Juego
 
> El jugador asume el rol de un Invocador, desplegando estratégicamente unidades sobre el tablero con el objetivo de destruir al Invocador enemigo y colapsar sus dominios.

---

## Concepto del Juego

### Tablero y losas

> El juego se desarrolla sobre un tablero de losas hexagonales (con 6 lados), donde cada jugador despliega sus piezas estratégicamente. El diseño hexagonal permite una movilidad amplia en seis direcciones, lo que genera múltiples posibilidades tácticas.

### Objetivo del juego

Hay dos formas principales de ganar:

1. Derrotar al Invocador enemigo y a todos sus héroes.
2. Dominar completamente el territorio enemigo, impidiendo que pueda invocar nuevas piezas o formar un dominio real.

###  Piezas y el Invocador

- Cada jugador comienza con una pieza única, el Invocador, y tres piesas simples de su elección.

- El Invocador representa al jugador y es esencial para mantener el dominio real del territorio.

- Si el Invocador muere, el jugador pierde, a menos que se cumplan ciertas condiciones de recuperación del dominio (ver más abajo).

### Dominio Posible y Dominio Real

- Cada pieza genera un dominio posible, es decir, el área que puede alcanzar o influenciar según sus capacidades de movimiento o de habilidad.
    - Por ejemplo, un soldado básico domina solo las dos losas al frente.
- Cuando varias piezas con dominio amplio coexisten en el tablero y sus dominios se superponen, forman un dominio real. Si una de las piezas es destruida el dominio real se pierde.
- Solo dentro del dominio real se pueden invocar nuevas piezas.
- Solo el Invocador tiene un dominio real por existir, los demas dominios reales se deben formar por la union de varios dominios posibles.

### Energía e invocación

- Cada jugador dispone de energía, un recurso que se usa para invocar piezas.
- Cada tipo de pieza tiene un coste de invocación.
- La energía se puede generar por habilidades de ciertas piezas, por ejemplo:
    - El invocador cada ciclo genera cierta cantidad de energía.
    - Hay piezas que cada x ciclos genera y cantidad de energía.
    - Hay piezas que al ser destruidas generan cierta cantidad de energía.
    - Hay piezas que al evolucionar genera energia una vez.
    - Hay piezas que al evolucionar, se transforman en otro tipo de pieza que si genera energía cada cierta cantida de ciclos.

### Ciclos y comportamiento de las piezas

- El juego avanza por ciclos (turnos), y cada pieza tiene su propio contador de ciclos. (en pantalla habria un contador que dice el tiempo de ciclo, digamos 3 min, y cada pieza tiene un contador propio si sus habilidades se cuentas por X ciclos, entonces tendras x espacios y cada cilo se llenara uno hasta que este completo, hara su habilidad y volvera a cero)
- Las habilidades, movimientos o transformaciones de una pieza dependen de su ciclo actual.
- Uno como invocador puede elegir el comportamiento automatico de cada pieza, por ejemplo: un estrategia agresiva seria que avanzaran al enemigo mas cercano, otra seria que defendieran al invocador, otra seria que se expandieran por el tablero.
- Mientras dura el ciclo se podra elegir: el movimiento de la pieza de forma manual o seleccionar un grupo y definirles una estrategia a seguir.

### Héroes

- Son piezas avanzadas con habilidades únicas.
- Requieren condiciones específicas para ser invocados (como energía, ciclo, dominio real, etc.).
- Si el Invocador muere pero hay un héroe activo o un nuevo dominio real formado (por ejemplo, al juntar tres Caster que solapan sus dominios), el jugador puede seguir en la partida.

### Combate

- Cada pieza tiene tres atributos:
    - Ataque
    - Defensa
    - Vida
- El ataque reduce la vida del objetivo primero.
- La defensa absorve parte del ataque.
    - Si el ataque es 10, y la defensa es 10, pasan 2 y la defensa se reduce en 8.
    - Si la defensa es 0, el siguiente ciclo se regenera 3, hasta que la barra este completa
- Si la vida se reduce a cero, la pieza es destruida.
- La vida no se regenera como la defensa, solo piezas especiales pueden regenerar vida.

### Tipos de piezas y estrategias

- Las piezas tienen roles asimétricos: algunas generan energía, otras evolucionan, otras dominan mucho terreno, otras no obedecen.
- Hay interacciones de ventaja y desventaja entre tipos.
- Esto permite a los jugadores:
    - Diseñar ejércitos personalizados.
    - Crear estrategias únicas de control, expansión o agresión.

### Territorio y cierre de espacios

- Si una pieza enemiga invade un dominio real, no muere automáticamente. Sino que queda a mercer de las habilidades especiales que tiene la pieza que genera el dominio real.
- Pero si la pieza enemiga queda encerrada sin espacio libre y no puede formar un nuevo dominio real por sí misma, comenzará a recibir daño constante cada ciclo hasta morir.
- El invocador es el unico que tiene un dominio real de forma natural.

### Síntesis del loop

- Cada pieza tiene su propio ciclo interno.
- Las acciones que puede realizar dependen de ese contador: moverse, atacar, invocar, evolucionar, explotar, etc.
- El core loop del juego gira en torno al manejo de ciclos, energía, dominio y posición.

---

## Inspiraciones

Lista de juegos o medios que inspiran mi idea:

| Nombre | ¿Por qué me inspira? |
|-------|---------------------------|
| Conway’s Game of Life | Me inspira el sistema de ciclos en el que, turno tras turno, cada celda es evaluada según su estado actual y el de sus celdas vecinas. Esta lógica de vida, muerte o expansión según reglas fijas y el entorno inmediato genera patrones complejos a partir de reglas simples. Me atrae especialmente el concepto de que cada unidad “decida” su destino en función del contexto que la rodea.|
|Fate/stay night|Me gusta cómo cada “rol” o “clase” tiene una personalidad marcada, habilidades distintas y un conjunto único de reglas para interactuar con el mundo o con otros personajes. La asimetría estratégica entre roles (como Saber, Archer, Berserker, etc.) me resulta fascinante, ya que permite que cada jugador o personaje tenga una experiencia distinta según su estilo.|
|Ajedrez| Me atrae la noción del tablero como un campo de duelo jerárquico, donde cada pieza tiene un valor simbólico y mecánico distinto. Además, ciertas piezas pueden evolucionar (como el peón que llega al otro extremo y se transforma en una reina), lo que introduce una idea de progreso condicional que podría integrarse en ciclos de juego estratégicos.|
|Go|El Go destaca por su profunda complejidad estratégica y por cómo el control del terreno puede determinar el curso de la partida. Me interesa su enfoque en la ocupación y dominio espacial más que en la eliminación directa, así como su capacidad para generar tensión y decisiones significativas con reglas muy simples.|
|Magic: The Gathering | Este juego me inspira por sus mecánicas de energía, invocación y personalización de estrategias. La diversidad de efectos, tipos de cartas y ritmos de turno ofrece una riqueza táctica que me gustaría capturar, especialmente la sensación de que el jugador puede armar su estilo y su camino a la victoria con mucha flexibilidad.|

---

## Objetivos del Desarrollo

- [ ] Planificar y desarrollar una base  
- [ ] Crear arte minimalista 2D  
- [ ] Implementar música o sonido ambiente  
- [ ] ~~Terminar una build jugable para el último día~~  
- [ ] Formar el tablero  
- [ ] Desarrollar las piezas  
- [ ] Que el turno tenga un ciclo con temporizador  
- [ ] Definir la táctica general de un grupo de piezas  
- [ ] Poner piezas en el tablero  
- [ ] Que las piezas tengan un ciclo interno  
- [ ] Que las piezas apliquen su habilidad cuando el ciclo lo indique  
- [ ] Poder mover la pieza de forma manual  
- [ ] Que si no muevo la pieza, esta se mueva según la estrategia general  
- [ ] Que una pieza pueda evolucionar  
- [ ] Calcular el daño de ataques o habilidades  
- [ ] Que una pieza pueda morir  
- [ ] Ver las posibles celdas en las que se puede mover una pieza  
- [ ] Ver los dominios reales de cada invocador  
- [ ] Incluir música libre de derechos (sin copyright) 
- [ ] Crear UI básica con indicadores de turno, timer y energía
- [ ] Implementar efectos visuales simples (ataques, habilidades, muerte)
- [ ] Guardar y cargar estado de partida (opcional)
- [ ] Añadir animaciones de movimiento o habilidades
- [ ] Crear un sistema de niveles o dificultad
- [ ] Balancear estadísticas de piezas (ataque, defensa, velocidad, etc.)
- [ ] Documentar reglas básicas dentro del juego
---

## Mecánicas Principales

- **Invocación de piezas**  
  El jugador puede invocar nuevas unidades gastando recursos o en intervalos definidos.

- **Formación y colocación en el tablero**  
  El jugador posiciona estratégicamente las piezas sobre un tablero dividido en celdas.

- **Ciclo de turnos con temporizador**  
  El juego avanza en ciclos de tiempo real o por turnos cronometrados.

- **Ciclo interno de las piezas**  
  Cada pieza tiene un temporizador interno que activa sus habilidades o efectos especiales.

- **Habilidades automáticas y activas**  
  Las piezas pueden ejecutar habilidades al completarse su ciclo, o el jugador puede activarlas directamente.

- **Movimiento manual o automatizado**  
  El jugador puede mover piezas directamente o dejar que se muevan según una táctica predefinida.

- **Evolución de piezas**  
  Las piezas pueden evolucionar tras ciertas condiciones, mejorando sus estadísticas o habilidades.

- **Cálculo de daño y combate**  
  Al enfrentarse a piezas enemigas, se calcula el daño según estadísticas, habilidades y modificadores.

- **Muerte de piezas**  
  Las piezas pueden ser eliminadas del tablero al perder toda su vida.

- **Visualización de celdas disponibles**  
  El jugador puede ver en qué celdas puede moverse una pieza antes de realizar una acción.

- **Dominio del invocador**  
  Cada jugador posee dominios que representan su control sobre el tablero. Estos pueden ser conquistados o destruidos.

- **Música y sonidos atmosféricos**  
  Ambientación sonora inmersiva con música libre de derechos.

- **Tácticas generales por grupo**  
  El jugador puede asignar comportamientos tácticos a grupos de piezas (ej. agresivo, defensivo, apoyo).

- **Defensa del núcleo / invocador**  
  Objetivo de proteger tu núcleo y destruir el del enemigo.

- **Territorio y expansión**  
  Controlar más del tablero da ventajas o recursos extra.

- **Piezas únicas y personalizables**  
  Las unidades tienen características propias y pueden recibir mejoras o ajustes.

---

## ~~Plan de Trabajo: 4 días~~

| Día   | Enfoque                   | Tareas clave                                     |
|-------|---------------------------|--------------------------------------------------|
| Día 1 | Preproducción + Prototipo | Idea, loop, movimiento, timers                   |
| Día 2 | Mecánicas centrales       | Eventos que se repiten, reinicio del ciclo       |
| Día 3 | Arte + Sonido + Pulido    | Diseños finales, efectos visuales y SFX          |
| Día 4 | Pruebas + Build final     | Corrección de errores, exportar, subir           |

---

## Hitos (Checkpoints)

- [ ] Loop funcional básico implementado
- [ ] Crear arte minimalista 2D
- [ ] Música o sonido ambiental funcional
- [ ] Formar el tablero de juego
- [ ] Crear piezas iniciales
- [ ] Implementar sistema de turnos con temporizador
- [ ] Permitir colocar piezas en el tablero
- [ ] Desarrollar el ciclo interno de cada pieza
- [ ] Ejecutar habilidades de piezas según su ciclo
- [ ] Movimiento manual de piezas
- [ ] Movimiento automático si no se elige manual
- [ ] Definir tácticas generales por grupo
- [ ] Implementar evolución de piezas
- [ ] Calcular daño entre piezas
- [ ] Eliminar pieza si muere
- [ ] Mostrar posibles celdas de movimiento
- [ ] Mostrar dominios reales
- [ ] Agregar música libre de derechos de autor
- [ ] Ajustar balance general del juego
- [ ] Pruebas de jugabilidad y feedback

---

## Notas 

En la gran mayoría de obras que usan loops temporales, el motivo central suele girar en torno a evitar una tragedia, resolver un misterio o lograr una transformación personal, y muchas veces todo a la vez.

### Tramas más comunes en historias con loops
| Tipo de Loop	| Objetivo narrativo común
|--------------------|------------------------------------|
|Evitar la muerte| Salvarse a sí mismo o a otro personaje de una muerte repetida | 
| Resolver un misterio| Usar el bucle para investigar y encontrar la verdad |
| Corregir el pasado|Cambiar una decisión clave para evitar un evento catastrófico | 
| Salvar el mundo | El loop ocurre antes de un apocalipsis o gran desastre |
| Transformación personal|El protagonista debe madurar o cambiar su perspectiva |
| Perspectivas múltiples|Se revive el mismo evento desde distintos personajes o cuerpos|
|Loop sobrenatural o cósmico | El ciclo se debe a una maldición, culto o fenómeno inexplicable|
|Clones / Automatización | Repeticiones sirven para colaborar contigo mismo (tipo puzle)|

### ¿Qué quiero hacer?

Ya que la mayoría de las tramas se centran en “revivir hasta hacerlo bien”, yo quiero enfatizar en:
- Loops no temporales, sino estratégicos o estructurales.
- Piezas/Unidades que tienen sus propios ciclos internos: como si cada entidad viviera su “loop de desarrollo” (cada 3 turnos gana habilidades, muta, se fragmenta, etc.).
- Usar el concepto de ciclo como recurso, no como historia.
