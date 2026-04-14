# Unidad 6

## Bitácora de proceso de aprendizaje
### Actividad 1

<img width="768" height="768" alt="image" src="https://github.com/user-attachments/assets/a39f910b-85d6-4a12-bc37-a9cb6bb4cfa8" />
#### Imagen 1 (puntos)
* Composición
Organización en flujos curvos que cruzan la imagen, como caminos o corrientes.
* Densidad
Alta y bastante uniforme, con zonas de concentración de color que destacan.
* Dirección del movimiento
Movimiento orgánico y curvo, siguiendo trayectorias suaves.
* Color
Base neutra (blanco/beige) con acentos de color agrupados en líneas o clusters.
* Ritmo
Ritmo constante por repetición de puntos, con variaciones que generan dinamismo.
* Repetición y variación
Mismo módulo (punto), pero cambia color, agrupación y dirección.
* Hipótesis
Sistema basado en:
* Campo vectorial o ruido (tipo Perlin)
* Los puntos siguen direcciones suaves.
* El color depende de posición o agrupación.


#### Imagen 2 (líneas)
* Composición
Estructura vertical y minimalista, dominada por líneas.
* Densidad
Media-baja, con mucho espacio vacío.
* Dirección del movimiento
Movimiento vertical, con ligeras ondulaciones.
* Color
Paleta reducida: rosado (fondo) + azul (líneas).
* Ritmo
Ritmo lento y repetitivo, con pequeñas variaciones en separación.
* Repetición y variación
Módulo repetido (línea), variando en posición, grosor y curvatura.
* Hipótesis
Sistema basado en:
* Generación de líneas verticales
* Uso de ruido para desplazar y deformar
* Variación controlada en posición y grosor


### Actividad 2
Un **agente autónomo** es una entidad que percibe su entorno, toma decisiones propias y actúa sin que alguien controle cada uno de sus movimientos. En lugar de decirle exactamente qué hacer, se le definen reglas de comportamiento, y a partir de ellas genera acciones y trayectorias por sí mismo.

Una **steering force** es una fuerza que guía el movimiento de un agente en tiempo real, ajustando su dirección y velocidad según ciertos objetivos o comportamientos, como seguir un punto, evitar obstáculos o alinearse con otros. Es más una “intención de movimiento” que una fuerza fija.

La diferencia entre una **steering force** y una fuerza externa como la gravedad es que la gravedad es constante, siempre actúa igual y no depende del contexto, mientras que la steering force es adaptable y cambia según la situación del agente, combinando distintas decisiones o comportamientos.

Estas ideas son útiles para el diseño visual porque permiten crear sistemas dinámicos donde el movimiento y las formas emergen de reglas simples, generando resultados orgánicos, variados e interactivos. Así, no solo se diseña la apariencia, sino también el comportamiento en el tiempo.

### Actividad 3
#### ¿Cómo está construido el campo de flujo?

El campo de flujo se construye como una **grilla (2D array) de vectores**, donde el espacio del canvas se divide en celdas según una resolución. Cada celda contiene un vector que indica una dirección, y estos vectores se generan mediante reglas como valores constantes, aleatorios o usando **ruido Perlin** para crear patrones suaves y naturales.

#### ¿Qué representa cada celda o vector del campo?

Cada celda representa una **dirección de movimiento en ese punto del espacio**. Es como una flecha invisible que le dice a cualquier agente: “si estás aquí, muévete en esta dirección”.

#### ¿Cómo usa un agente su posición para consultar el campo?

El agente toma su posición (x, y) y la divide por la resolución del campo para obtener la **columna y fila** correspondientes en la grilla. Así puede acceder al vector específico de esa zona del espacio.

#### ¿Cómo se convierte el vector consultado en una decisión de movimiento?

El agente usa ese vector como su **velocidad deseada**, lo ajusta a su velocidad máxima y luego calcula una **steering force** restando su velocidad actual. Esa fuerza se limita y se aplica, generando un movimiento suave y progresivo hacia la dirección indicada.

#### Parámetros importantes del sistema

* Resolución: define el tamaño de cada celda; afecta el nivel de detalle del campo.
* maxspeed: velocidad máxima del agente; controla qué tan rápido se mueve.
* maxforce: límite de fuerza; determina qué tan bruscos o suaves son los cambios.
* Cantidad de agentes: influye en la complejidad visual y densidad del sistema.

#### Modificación y efecto visual

Si se agrega una tercera dimensión al ruido (noise(x, y, tiempo)), el campo cambia con el tiempo. Esto produce un efecto visual de **flujo dinámico**, donde las trayectorias evolucionan constantemente, generando una sensación de viento vivo o corrientes en movimiento.

#### ¿Qué tipo de movimiento produce este algoritmo?

Produce un movimiento **orgánico, fluido y continuo**, similar a corrientes de agua, viento o humo, donde los agentes siguen trayectorias suaves en lugar de líneas rígidas.

#### ¿Qué sensaciones visuales sugiere?

Genera sensaciones de:

* fluidez
* calma o caos controlado (según parámetros)
* naturaleza (ríos, aire, energía)
* sistemas vivos y dinámicos

#### ¿En qué tipo de pieza musical funcionaría bien?

Encajaría muy bien en música:

* ambient
* electrónica suave
* experimental
* lo-fi o chill


### Actividad 4

#### Tres reglas básicas del flocking
* Separación
Es la regla que hace que cada agente evite chocar con los demás. Si otros están muy cerca, se aleja. Esto mantiene una distancia mínima entre ellos.
* Alineación
El agente intenta moverse en la misma dirección y velocidad que sus vecinos cercanos. Es lo que hace que el grupo se vea coordinado.
* Cohesión
El agente se mueve hacia el centro del grupo, es decir, hacia la posición promedio de sus vecinos. Esto evita que el grupo se disperse.

#### Parámetros que controlan estas reglas
* neighborDistance: qué tan lejos puede “ver” cada agente
* Pesos (multipliers): qué tan fuerte es cada regla (separation, alignment, cohesion)
* maxspeed: velocidad máxima
* maxforce: qué tan brusco puede cambiar de dirección
* Cantidad de boids: tamaño del grupo

#### Modificación y efecto

* Si aumentas el peso de separación (por ejemplo 1.5 → 3.0):
  * Los agentes se alejan más entre sí
  * El grupo se vuelve más disperso y nervioso
* Si aumentas cohesión:
  * Los agentes se agrupan más
  * El flock se vuelve más compacto
* Si aumentas alineación:
  * Todos se mueven más sincronizados
  * Se ve más ordenado y fluido

#### Comportamiento emergente
* Dependiendo de los parámetros, el sistema puede ser:
  * Compacto: si domina la cohesión
  * Disperso: si domina la separación
  * Estable: si hay buen balance entre las tres reglas
  * Nervioso: si hay mucha fuerza o cambios bruscos (maxforce alto)
  * Caótico: si los pesos están desbalanceados
  * Fluido: si todo está equilibrado (el caso más natural)

#### ¿Qué atmósfera visual produce?
El flocking genera una atmósfera de:
* vida colectiva
* inteligencia emergente
* movimiento orgánico
Se siente como:
* bandadas de aves
* bancos de peces
* sistemas naturales en armonía

#### ¿Con qué tipo de música funciona mejor?
Funciona muy bien con:
* ambient → movimientos suaves y fluidos
* electrónica orgánica → patrones repetitivos pero vivos
* post-rock / instrumental → crecimiento y dinámica colectiva
* techno suave → sincronización rítmica del grupo

### Actividad 5

#### Tipo de movimiento que producen:
Los flow fields generan un movimiento continuo, fluido y direccional, donde los agentes siguen trayectorias definidas por un campo, similar a corrientes de agua o viento; en cambio, el flocking produce un movimiento colectivo y orgánico basado en la interacción entre agentes, formando grupos dinámicos que se agrupan, separan y reorganizan constantemente.

#### Nivel de control visual:
En los flow fields el control visual es alto, ya que puedes diseñar directamente las direcciones del movimiento manipulando el campo; mientras que en el flocking el control es más indirecto, porque defines reglas y parámetros, pero el resultado final emerge de la interacción entre los agentes, haciéndolo menos predecible.

#### Nivel de emergencia:
Los flow fields tienen un nivel de emergencia medio, ya que aunque hay variación, el comportamiento sigue una estructura definida; por otro lado, el flocking tiene un nivel de emergencia alto, porque patrones complejos surgen de reglas simples sin un control central.

#### Tipo de atmósfera o sensación:
Los flow fields generan sensaciones de fluidez, calma o energía constante, evocando fenómenos naturales como el viento o el agua; en contraste, el flocking produce una atmósfera de vida colectiva, inteligencia grupal y tensión entre orden y caos.

#### Relación posible con una pieza musical:
Los flow fields funcionan mejor con música ambient o suave, donde el flujo continuo acompaña la atmósfera sonora; mientras que el flocking se adapta mejor a música con ritmo o energía, ya que su comportamiento colectivo puede sincronizarse con cambios e intensidades musicales.

### Ventajas y limitaciones:
Los flow fields ofrecen gran control y coherencia visual, siendo ideales para composiciones dirigidas, pero pueden volverse repetitivos y menos dinámicos; en cambio, el flocking destaca por su complejidad emergente y sensación de sistema vivo, aunque es más difícil de controlar y puede volverse caótico si no se equilibran bien sus parámetros.
## Bitácora de aplicación 


## Bitácora de reflexión
