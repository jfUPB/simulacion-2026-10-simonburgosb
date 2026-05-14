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

#### Concepto visual

La pieza representa una mente atrapada en un bucle emocional, donde los recuerdos, la obsesión y la pérdida se repiten sin resolverse. Visualmente, esto se traduce en un sistema de agentes que giran, se agrupan y se desintegran constantemente, sin llegar nunca a estabilizarse.

#### Relación con el tema musical

La canción tiene:
* tristeza → dispersión
* rabia → tensión y caos
* obsesión → repetición de patrones

Traducción visual:
* Partes suaves: agentes lentos, dispersos
* Partes intensas: flocking fuerte, compresión


#### Moodboard

<img width="736" height="1308" alt="image" src="https://github.com/user-attachments/assets/3700ced8-cce3-417c-b092-e4b1433d83b8" />
<img width="736" height="1104" alt="image" src="https://github.com/user-attachments/assets/236af6b3-7cc6-46c7-a935-c5c215390cfd" />
<img width="676" height="1200" alt="image" src="https://github.com/user-attachments/assets/1ee43b3b-e7fc-460f-a81f-aa1feae0462f" />
<img width="736" height="1051" alt="image" src="https://github.com/user-attachments/assets/8cb40ff9-75e6-49c3-929e-d0565214a237" />
<img width="736" height="708" alt="image" src="https://github.com/user-attachments/assets/9160472e-0ce7-4462-8182-65c2a5fd20b8" />

#### Bocetos
<img width="1600" height="785" alt="image" src="https://github.com/user-attachments/assets/5668a22c-ec05-41de-906b-18a5030f03d7" />

#### Mapa de decisiones
* Fondo oscuro → introspección
* Flow field → memoria constante / flujo emocional
* Flocking → obsesión y apego
* Baja cohesión inicial → inestabilidad
* Pulsos en graves → latido emocional
* Trails (rastros) → recuerdos que no desaparecen

#### Mapa de interpretación
* Click: ruptura emocional
* A/S/D: estados emocionales
* Audio: energía general del sistema


#### Justificacion del algoritmo
El uso combinado de flow fields y flocking responde a la necesidad de representar dos dimensiones emocionales distintas presentes en la canción “Qué vuelta Vox”. Por un lado, el flow field permite construir una sensación de flujo constante y repetitivo, que se asocia con el pensamiento obsesivo y la imposibilidad de salir de un estado emocional. Este algoritmo aporta continuidad, suavidad y una dirección general, funcionando como una metáfora del paso del tiempo y de los recuerdos que siguen circulando sin resolverse.

Por otro lado, el flocking introduce una capa de comportamiento colectivo que representa la tensión emocional, el apego y la necesidad de cercanía. A través de sus reglas de cohesión, alineación y separación, los agentes se agrupan, se dispersan y se reorganizan, generando dinámicas que evocan relaciones inestables, momentos de conexión y rupturas

#### Reactividad al audio
* Amplitud (volumen):
controla velocidad y dispersión
* Graves:
generan pulsos de contracción (como latidos emocionales)
* Agudos:
afectan jitter/movimiento nervioso

#### Evidencia de la IA
En este proyecto la IA se utilizo como apoyo tecnico, ya que el tema de las visuales, su interpretacion, reactiividad con el audio sistema de movimientso, modos, significados/relaciones e intereacciones fueron hechas por mi. 

Específicamente, la IA se empleó para:
* Resolver errores técnicos relacionados con reproducción de audio, uso de p5.FFT y p5.Amplitude.
* Optimizar y organizar el código, facilitando la integración entre flocking y flow fields.
* Proponer mejoras en los parametros para mayor notoriedad de la reactividad del audio.

#### Codigo 

``` js
let boids = [];
let flow;
let cols, rows;
let resolution = 20;

let song;
let fft, amp;

let mode = "flow"; 

function preload() {
  song = loadSound('Feid.mp3'); 
}

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);

  cols = floor(width / resolution);
  rows = floor(height / resolution);

  flow = new FlowField();

  for (let i = 0; i < 150; i++) {
    boids.push(new Boid(random(width), random(height)));
  }

  fft = new p5.FFT();
  amp = new p5.Amplitude();

  fft.setInput(song);
  amp.setInput(song);

  userStartAudio();
}

function draw() {
  // TRAIL (efecto memoria)
  fill(0, 30);
  noStroke();
  rect(0, 0, width, height);

  let level = amp.getLevel() * 3;
  let bass = fft.getEnergy("bass");
  let treble = fft.getEnergy("treble");

  flow.update();

  for (let b of boids) {

    if (mode === "flow") {
      let f = flow.lookup(b.position);
      b.applyForce(f);
    }

    if (mode === "flock") {
      b.flock(boids);
    }

    if (mode === "chaos") {
      let f = flow.lookup(b.position);
      b.applyForce(f);
      b.flock(boids);
      b.applyForce(p5.Vector.random2D().mult(0.5));
    }

    b.maxspeed = map(level, 0, 1, 2, 6);
    b.maxforce = map(treble, 0, 255, 0.05, 0.5);

    if (bass > 180) {
      let explosion = p5.Vector.random2D().mult(5);
      b.applyForce(explosion);
    }

    b.update();
    b.edges();
    b.show();
  }
}

let started = false;

function mousePressed() {

  if (!started) {
    fullscreen(true);

    if (!song.isPlaying()) {
      song.loop();
    }

    started = true;
  }

  for (let b of boids) {
    let force = p5.Vector.sub(b.position, createVector(mouseX, mouseY));
    force.setMag(3);
    b.applyForce(force);
  }
}

function keyPressed() {
  if (key === 'A') mode = "flow";
  if (key === 'S') mode = "flock";
  if (key === 'D') mode = "chaos";
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);

  cols = floor(width / resolution);
  rows = floor(height / resolution);

  flow = new FlowField(); 
}



class FlowField {
  constructor() {
    this.field = new Array(cols);
    for (let i = 0; i < cols; i++) {
      this.field[i] = new Array(rows);
    }
    this.zoff = 0;
  }

  update() {
    let xoff = 0;
    for (let i = 0; i < cols; i++) {
      let yoff = 0;
      for (let j = 0; j < rows; j++) {
        let angle = map(noise(xoff, yoff, this.zoff), 0, 1, 0, TWO_PI);
        this.field[i][j] = p5.Vector.fromAngle(angle);
        yoff += 0.1;
      }
      xoff += 0.1;
    }
    this.zoff += 0.01;
  }

  lookup(pos) {
    let col = constrain(floor(pos.x / resolution), 0, cols - 1);
    let row = constrain(floor(pos.y / resolution), 0, rows - 1);
    return this.field[col][row].copy();
  }
}



class Boid {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.velocity = p5.Vector.random2D();
    this.acceleration = createVector(0, 0);

    this.maxspeed = 3;
    this.maxforce = 0.1;
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  flock(boids) {
    let sep = this.separate(boids).mult(1.5);
    let ali = this.align(boids).mult(1.0);
    let coh = this.cohesion(boids).mult(1.0);

    this.applyForce(sep);
    this.applyForce(ali);
    this.applyForce(coh);
  }

  separate(boids) {
    let desiredSeparation = 25;
    let steer = createVector(0, 0);
    let count = 0;

    for (let other of boids) {
      let d = dist(this.position.x, this.position.y, other.position.x, other.position.y);
      if (d > 0 && d < desiredSeparation) {
        let diff = p5.Vector.sub(this.position, other.position);
        diff.normalize();
        diff.div(d);
        steer.add(diff);
        count++;
      }
    }

    if (count > 0) steer.div(count);

    if (steer.mag() > 0) {
      steer.setMag(this.maxspeed);
      steer.sub(this.velocity);
      steer.limit(this.maxforce);
    }

    return steer;
  }

  align(boids) {
    let neighborDist = 50;
    let sum = createVector(0, 0);
    let count = 0;

    for (let other of boids) {
      let d = p5.Vector.dist(this.position, other.position);
      if (d > 0 && d < neighborDist) {
        sum.add(other.velocity);
        count++;
      }
    }

    if (count > 0) {
      sum.div(count);
      sum.setMag(this.maxspeed);
      let steer = p5.Vector.sub(sum, this.velocity);
      steer.limit(this.maxforce);
      return steer;
    }

    return createVector(0, 0);
  }

  cohesion(boids) {
    let neighborDist = 50;
    let sum = createVector(0, 0);
    let count = 0;

    for (let other of boids) {
      let d = p5.Vector.dist(this.position, other.position);
      if (d > 0 && d < neighborDist) {
        sum.add(other.position);
        count++;
      }
    }

    if (count > 0) {
      sum.div(count);
      return this.seek(sum);
    }

    return createVector(0, 0);
  }

  seek(target) {
    let desired = p5.Vector.sub(target, this.position);
    desired.setMag(this.maxspeed);
    let steer = p5.Vector.sub(desired, this.velocity);
    steer.limit(this.maxforce);
    return steer;
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxspeed);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  edges() {
    if (this.position.x > width) this.position.x = 0;
    if (this.position.x < 0) this.position.x = width;
    if (this.position.y > height) this.position.y = 0;
    if (this.position.y < 0) this.position.y = height;
  }

  show() {
    stroke(0, 255, 150, 120); 
    strokeWeight(2);
    point(this.position.x, this.position.y);
  }
}
```

#### Enlace al Sketch
https://editor.p5js.org/simonburgosb/sketches/4QowVfvNG


#### Capturas del codigo
<img width="881" height="671" alt="image" src="https://github.com/user-attachments/assets/a807fe46-c3f3-49d0-92dc-d6ef2cc8d8b5" />

<img width="901" height="452" alt="image" src="https://github.com/user-attachments/assets/891c2464-d002-4e55-94c2-1ca7ce6caffc" />




## Bitácora de reflexión
