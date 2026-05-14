# Unidad 2

## Bitácora de proceso de aprendizaje
### Actividad 1
Qué me gusta de este tipo de trabajo: https://openprocessing.org/sketch/143842 
Estilo generativo e interactivo
Las obras que exploran ruido, turbulencia o patrones generativos suelen ser muy atractivas porque combinan estética con comportamiento algorítmico. La interacción con el usuario (por ejemplo, mover el mouse para influenciar la visualización) hace que cada ejecución sea única e invita a explorar. Este enfoque es excelente para experimentar con código visual y aprender conceptos de lógica y gráficos.
### Actividad 2
En matemáticas, sumar dos vectores es algo así:
* (x1, y1) + (x2,y2) = (x1*x2, y1*y2)
Porque en JavaScript el operador + no sabe sumar objetos.

### Actividad 3

Tuve que modificiar la forma en como da el step 
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

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
    this.position = createVector(width / 2, height / 2)
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    stroke(0);
    point(this.position);
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.position.x++;
    } else if (choice == 1) {
      this.position.x--;
    } else if (choice == 2) {
      this.position.y++;
    } else {
      this.position.y--;
    }
    this.position.x = constrain(this.position.x, 0, width, -1)
    this.position.y = constrain(this.position.y, 0, height, -1)
    
  }
}
```
### Actividad 4

#### ¿Qué resultado esperas obtener en el programa anterior?
Que el programa imprima el cmabio del vector y ademas imprima el only once
#### ¿Qué resultado obtuviste?
Justo ese
Recuerda los conceptos de paso por valor y paso por referencia en programación.
#### ¿Qué tipo de paso se está realizando en el código?
Paso por referencia
#### ¿Qué aprendiste?
Que con un vector se puede hacer un paso por referencia para modificar el valor
## Bitácora de aplicación 

### Actividad 5

* El método mag() devuelve la longitud (magnitud) de un vector.
* mag() devuelve la longitud real. magSq() devuelve la magnitud al cuadrado.
* normalize() convierte un vector en uno unitario — es decir, con longitud 1, pero mantiene la misma dirección.
* El método dot() mide cuánta proyección tiene un vector sobre otro, diciendo qué tan alineados están.
* La estática no modifica ninguno de los vectores. La de instancia opera sobre el vector al que fue llamada.
* El producto cruz de dos vectores genera un tercer vector perpendicular al plano de los dos originales, y cuya longitud es proporcional al área del paralelogramo formado por ellos.
* dist() calcula la distancia entre dos vectores
* normalize(): Te da un vector de longitud 1. limit(max): Restringe la longitud máxima de un vector.

### Actividad 6
``` js
let t = 0;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(200);

  let v0 = createVector(50, 50);
  let v1 = createVector(100, 0);   // rojo
  let v2 = createVector(0, 100);   // azul

  // t oscila suavemente entre 0 y 1
  let amt = (sin(t) + 1) / 2;

  let v3 = p5.Vector.lerp(v1, v2, amt);

  drawArrow(v0, v1, color('red'));
  drawArrow(v0, v2, color('blue'));
  drawArrow(v0, v3, lerpColor(color('red'), color('blue'), amt));

  t += 0.05;
}

function drawArrow(base, vec, myColor) {
  push();
  stroke(myColor);
  strokeWeight(6);
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
* lerp() significa linear interpolation (interpolación lineal).
* lerpColor() hace exactamente lo mismo… pero con colores
* Esta función usa transformaciones.

### Actividad 7
Motion 101 es el algoritmo más elemental de movimiento:
* Sumar la velocidad a la posición
* Dibujar el objeto en su nueva posición

Vectores como flechas
* La posición es un vector que apunta desde el origen hasta la ubicación actual del objeto.
* La velocidad es otro vector que indica dirección y rapidez de movimiento.

#### En el ejemplo 
``` js
update() {
  this.position.add(this.velocity);
}
```
Cada frame:
* Se suma la velocidad a la posición
* El objeto se desplaza exactamente ese vector

Si la velocidad no cambia:
* El movimiento es uniforme
* La trayectoria es una línea recta


### Actividad 8
#### Aceleracion Constante
* El objeto empieza lento
* Cada frame va más rápido
* Movimiento rectilíneo acelerado

#### Aceleracion aleatoria
* Movimiento tipo “borracho”
* Cambios bruscos de dirección
* No hay trayectoria estable

#### Aceleracion hacia el mouse
* El objeto “persigue” el cursor


## Bitácora de Aplicacion



#### Modo 1 — Aceleración hacia el mouse

* Regla: “todo quiere ir al hacia lo que destaca”
* Geométricamente: vector desde partícula → mouse

#### Modo 2 — Aceleración orgánica (noise)

* Regla: “el mundo empuja de forma suave y continua”
* No hay caos puro, hay coherencia local

#### Modo 3 — Aceleración orbital

* Regla: “la fuerza de empuje es tan grande como la vida misma”
* Se rota el vector → movimiento circular

``` js
let movers = [];

let mode = 1;

function setup() {
  // Crea el lienzo donde se dibuja la obra
  createCanvas(600, 400);

  // Crea 200 partículas
  for (let i = 0; i < 200; i++) {
    movers.push(new Mover());
  }
}

function draw() {
  // Fondo negro con transparencia para dejar estelas
  background(0, 30);

  // Recorre todas las partículas
  for (let m of movers) {
    m.applyAcceleration();
    m.update();
    m.edges();
    m.show();
  }
}

function keyPressed() {
  if (key === '1') mode = 1;
  if (key === '2') mode = 2;
  if (key === '3') mode = 3;
}

class Mover {
  constructor() {
    // Vector posición inicial aleatoria
    this.position = createVector(random(width), random(height));

    // Vector velocidad inicial con dirección aleatoria
    this.velocity = p5.Vector.random2D();

    // Vector aceleración (empieza en cero)
    this.acceleration = createVector(0, 0);

    // Límite máximo de velocidad
    this.maxSpeed = 4;
  }

  applyAcceleration() {
    // Decide qué regla de aceleración aplicar
    if (mode === 1) this.attractToMouse();
    if (mode === 2) this.noiseAcceleration();
    if (mode === 3) this.orbitalAcceleration();
  }

  attractToMouse() {
    // Vector que representa la posición del mouse
    let mouse = createVector(mouseX, mouseY);

    // Vector dirección desde la partícula hacia el mouse
    let dir = p5.Vector.sub(mouse, this.position);

    // Normaliza el vector para quedarte solo con la dirección
    dir.normalize();

    // Ajusta la intensidad de la aceleración
    dir.mult(0.2);

    // Asigna esa dirección como aceleración
    this.acceleration = dir;
  }

  noiseAcceleration() {
    // Calcula un ángulo usando ruido Perlin
    let angle = noise(
      this.position.x * 0.01, // variación espacial en x
      this.position.y * 0.01, // variación espacial en y
      frameCount * 0.01       // variación temporal
    ) * TWO_PI * 2;

    // Crea un vector unitario a partir del ángulo
    this.acceleration = p5.Vector.fromAngle(angle);

    // Escala la fuerza de la aceleración
    this.acceleration.mult(0.3);
  }

  orbitalAcceleration() {
    // Vector que representa la posición del mouse
    let mouse = createVector(mouseX, mouseY);

    // Vector desde la partícula hacia el mouse
    let dir = p5.Vector.sub(mouse, this.position);

    // Rota el vector 90° para que sea perpendicular (órbita)
    dir.rotate(HALF_PI);

    // Normaliza para controlar solo la dirección
    dir.normalize();

    // Ajusta la intensidad de la aceleración
    dir.mult(0.2);

    // Asigna la aceleración orbital
    this.acceleration = dir;
  }

  update() {
    // La aceleración cambia la velocidad
    this.velocity.add(this.acceleration);

    // Limita la velocidad máxima
    this.velocity.limit(this.maxSpeed);

    this.position.add(this.velocity);
  }

  show() {
    stroke(255, 150);
    strokeWeight(2);
    point(this.position.x, this.position.y);
  }

  edges() {
    // Si sale por la izquierda, entra por la derecha
    if (this.position.x < 0) this.position.x = width;

    // Si sale por la derecha, entra por la izquierda
    if (this.position.x > width) this.position.x = 0;

    // Si sale por arriba, entra por abajo
    if (this.position.y < 0) this.position.y = height;

    // Si sale por abajo, entra por arriba
    if (this.position.y > height) this.position.y = 0;
  }
}
```
https://editor.p5js.org/simonburgosb/sketches/VsFsx90t4
<img width="748" height="491" alt="image" src="https://github.com/user-attachments/assets/d04e4f9e-e6a8-4e00-bbfe-dfa8663a5461" />
<img width="737" height="495" alt="image" src="https://github.com/user-attachments/assets/504ee042-c81f-47eb-b0cc-16276fe83ac0" />

## Bitácora de reflexión

La obra representa un sistema de agentes que se mueven en un espacio compartido siguiendo reglas simples de movimiento (motion 101), pero cuya aceleración cambia según el contexto:

* A veces el sistema es estable (aceleración constante).
* A veces es caótico (aceleración aleatoria).
* A veces es dirigido (aceleración hacia el mouse).

Emergen patrones: agrupaciones, dispersión, corrientes y flujos visuales.

``` js
let movers = [];
let mode = 3;
let perceptionRadius = 60;

function setup() {
  createCanvas(600, 400);
  for (let i = 0; i < 150; i++) {
    movers.push(new Mover());
  }
}

function draw() {
  background(0, 25);

  for (let m of movers) {
    m.applyBehavior(movers);
    m.update();
    m.edges();
    m.show();
  }
}

function keyPressed() {
  if (key === '1') mode = 1; // atracción
  if (key === '2') mode = 2; // repulsión
  if (key === '3') mode = 3; // equilibrio
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = p5.Vector.random2D();
    this.acceleration = createVector(0, 0);
    this.maxSpeed = 3;
    this.maxForce = 0.05;
  }

  applyBehavior(others) {
    let steering = createVector(0, 0);
    let total = 0;

    for (let other of others) {
      let d = p5.Vector.dist(this.position, other.position);

      if (other !== this && d < perceptionRadius && d > 0) {
        let diff = p5.Vector.sub(other.position, this.position);

        if (mode === 2) diff.mult(-1); // repulsión

        diff.normalize();
        diff.div(d); // influencia decrece con distancia
        steering.add(diff);
        total++;
      }
    }

    if (total > 0) {
      steering.div(total);
      steering.setMag(this.maxSpeed);
      steering.sub(this.velocity);
      steering.limit(this.maxForce);
    }

    // Influencia sutil del mouse
    let mouse = createVector(mouseX, mouseY);
    let mouseForce = p5.Vector.sub(mouse, this.position);
    mouseForce.normalize();
    mouseForce.mult(0.02);

    this.acceleration = steering.add(mouseForce);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.velocity.limit(this.maxSpeed);
    this.position.add(this.velocity);
  }

  show() {
    stroke(255, 180);
    strokeWeight(1);
    point(this.position.x, this.position.y);
  }

  edges() {
    if (this.position.x < 0) this.position.x = width;
    if (this.position.x > width) this.position.x = 0;
    if (this.position.y < 0) this.position.y = height;
    if (this.position.y > height) this.position.y = 0;
  }
}
```
https://editor.p5js.org/simonburgosb/sketches/4jsy6TGH5

<img width="737" height="487" alt="image" src="https://github.com/user-attachments/assets/c52eee07-6112-46cf-9711-94b26e9f83dd" />
<img width="742" height="498" alt="image" src="https://github.com/user-attachments/assets/e5b87161-e88d-4fc6-b740-7175fe09c05e" />

