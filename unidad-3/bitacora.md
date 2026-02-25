# Unidad 3

## Bitácora de proceso de aprendizaje
### Actividad 1

La verdad me genero mucha incomidad he incertidumbre ya que es lo que se menciona en el video, "¿Para que Molestrase?"
Si ya todo se genera por IA y en segundo, uno puede tender a pensar para que gasta tiempo si igual va ser pensdo que fue hecho por IA, que bobada. Pero para mi va mas alla; el problema lo veo es a futuro y como esto me puede afectar al terminar mi carrera y la verdad que no me deja pensando en un futuro muy alentador. 

### Actividad 2
Entender que la aceleración es el resultado de todas las fuerzas aplicadas fue clave. Al aplicar fuerzas como viento y gravedad en cada frame mediante applyForce(), se hace evidente que el comportamiento del objeto es más natural y predecible. La aceleración deja de ser una variable “misteriosa” y se convierte en una consecuencia directa de lo que ocurre en el entorno.

Uno de los puntos más importantes fue comprender por qué es necesario reiniciar la aceleración al final del método update() usando this.acceleration.mult(0). Esto se hace porque las fuerzas solo deben influir durante un frame; si no se reinicia la aceleración, las fuerzas se acumularían indefinidamente, generando un movimiento irreal y descontrolado. Reiniciarla permite que en cada frame la aceleración represente únicamente las fuerzas actuales.

### Actividad 3

#### Friccion 
``` js
let mover;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
}

function draw() {
  background(255, 40);

  // Fricción
  let friction = mover.velocity.copy();
  friction.normalize();
  friction.mult(-0.05);

  mover.applyForce(friction);

  mover.update();
  mover.checkEdges();
  mover.show();
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, height / 2);
    this.velocity = p5.Vector.random2D().mult(5);
    this.acceleration = createVector();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  checkEdges() {
    if (this.position.x > width || this.position.x < 0) this.velocity.x *= -1;
    if (this.position.y > height || this.position.y < 0) this.velocity.y *= -1;
  }

  show() {
    fill(0);
    noStroke();
    circle(this.position.x, this.position.y, 16);
  }
}
```

#### Resistencia Al Aire

``` js
let mover;
let liquid;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
  liquid = new Liquid(0, height / 2, width, height / 2, 0.2);
}

function draw() {
  background(255);

  liquid.show();

  // Gravedad constante
  let gravity = createVector(0, 0.1);
  mover.applyForce(gravity);

  // Resistencia
  if (liquid.contains(mover)) {
    let drag = mover.velocity.copy();
    drag.normalize();
    let speed = mover.velocity.mag();
    drag.mult(-liquid.c * speed * speed);
    mover.applyForce(drag);
  }

  mover.update();
  mover.checkEdges();
  mover.show();
}

class Liquid {
  constructor(x, y, w, h, c) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.c = c;
  }

  contains(m) {
    return (
      m.position.x > this.x &&
      m.position.x < this.x + this.w &&
      m.position.y > this.y &&
      m.position.y < this.y + this.h
    );
  }

  show() {
    fill(200, 220, 255);
    noStroke();
    rect(this.x, this.y, this.w, this.h);
  }
}

class Mover {
  constructor() {
    this.position = createVector(width / 2, 20);
    this.velocity = createVector(2, 0);
    this.acceleration = createVector();
  }

  applyForce(force) {
    this.acceleration.add(force);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  checkEdges() {
    if (this.position.y > height) {
      this.position.y = 0;
      this.velocity.mult(0);
    }
  }

  show() {
    fill(0);
    circle(this.position.x, this.position.y, 16);
  }
}
```

#### Atraccion Gravitacional 
``` js
let mover;
let attractor;

function setup() {
  createCanvas(640, 240);
  mover = new Mover();
  attractor = new Attractor(width / 2, height / 2);
}

function draw() {
  background(255);

  let force = attractor.attract(mover);
  mover.applyForce(force);

  mover.update();
  mover.show();
  attractor.show();
}

class Attractor {
  constructor(x, y) {
    this.position = createVector(x, y);
    this.mass = 20;
    this.G = 1;
  }

  attract(m) {
    let force = p5.Vector.sub(this.position, m.position);
    let distance = constrain(force.mag(), 5, 25);
    force.normalize();

    let strength = (this.G * this.mass * m.mass) / (distance * distance);
    force.mult(strength);
    return force;
  }

  show() {
    fill(0);
    circle(this.position.x, this.position.y, 32);
  }
}

class Mover {
  constructor() {
    this.position = createVector(random(width), random(height));
    this.velocity = createVector();
    this.acceleration = createVector();
    this.mass = 1;
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    fill(150);
    circle(this.position.x, this.position.y, 12);
  }
}
```


## Bitácora de aplicación 

El concepto de la historia es que la energia se transforma pero nunca se destruye hasta llegar a un punto de unidad es por esos que la obra es como que siempre cobra vida. La obra generativa parte de una forma primordial: un círculo, símbolo de unidad, equilibrio y reposo. Esta forma inicial representa un sistema estable, sin tensiones externas. A medida que el usuario interactúa con la obra, se introduce una fuerza de estiramiento que actúa como un “jalón” desde el centro hacia el exterior, rompiendo progresivamente esa estabilidad inicial.

https://editor.p5js.org/simonburgosb/sketches/g4gNmZ4f5

``` js
let particles = [];
let center;
let mode = "mandala";

function setup() {
  createCanvas(600, 600);
  center = createVector(width / 2, height / 2);

  let total = 24;
  let baseRadius = 120;

  for (let i = 0; i < total; i++) {
    let angle = map(i, 0, total, 0, TWO_PI);
    particles.push(new Particle(angle, baseRadius));
  }
}

function draw() {
  background(245);

  for (let p of particles) {
    let target;

    if (mode === "mandala") {
      target = p.mandalaTarget();
    } else {
      target = p.circleTarget();
    }

    // Fuerza de atracción hacia el objetivo
    let force = p5.Vector.sub(target, p.position);
    force.mult(0.05);
    p.applyForce(force);

    // Fricción
    let friction = p.velocity.copy();
    friction.normalize();
    friction.mult(-0.2);
    p.applyForce(friction);

    p.update();
  }

  drawConnections();

  for (let p of particles) {
    p.show();
  }
}

function keyPressed() {
  if (keyCode === RIGHT_ARROW) {
    mode = "circle";
  }
  if (keyCode === LEFT_ARROW) {
    mode = "mandala";
  }
}

// -----------------------------------

class Particle {
  constructor(angle, radius) {
    this.angle = angle;
    this.radius = radius;

    this.position = this.mandalaTarget().copy();
    this.velocity = createVector();
    this.acceleration = createVector();
    this.mass = 1;
  }

  mandalaTarget() {
    // Forma tipo mandala mecánica
    let r = this.radius + sin(this.angle * 4) * 40;
    let x = center.x + cos(this.angle) * r;
    let y = center.y + sin(this.angle) * r;
    return createVector(x, y);
  }

  circleTarget() {
    // Forma círculo simple
    let r = 80;
    let x = center.x + cos(this.angle) * r;
    let y = center.y + sin(this.angle) * r;
    return createVector(x, y);
  }

  applyForce(force) {
    let f = p5.Vector.div(force, this.mass);
    this.acceleration.add(f);
  }

  update() {
    this.velocity.add(this.acceleration);
    this.position.add(this.velocity);
    this.acceleration.mult(0);
  }

  show() {
    noStroke();
    fill(200, 200, 30);
    circle(this.position.x, this.position.y, 6);
  }
}

// -----------------------------------

function drawConnections() {
  stroke(180, 0, 0, 140);
  noFill();
  beginShape();
  for (let p of particles) {
    vertex(p.position.x, p.position.y);
  }
  endShape(CLOSE);
}
```

<img width="520" height="493" alt="image" src="https://github.com/user-attachments/assets/a0f2cb0a-9c63-424e-92e8-84017be76a96" />

## Bitácora de reflexión

