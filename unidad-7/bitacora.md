# Unidad 7

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 
### Palabra elegida

BRISA

### Justificación conceptual

La palabra brisa representa un fenómeno natural sutil, constante y envolvente. A diferencia de fuerzas como el viento fuerte o la tormenta, la brisa no actúa de manera violenta, sino progresiva y casi imperceptible. Ademas de su relacion con la marca de agua.

El proyecto busca traducir esta cualidad a un sistema interactivo donde el movimiento no sea abrupto, sino orgánico, mediado y acumulativo. La intención es construir una experiencia donde el usuario no vea directamente la fuerza, sino sus efectos.

### Análisis de significado visual y comportamental
#### Visual:
* Ligereza
* Espacio entre elementos
* Transparencia / suavidad
* Movimiento fluido
* Ausencia de rigidez
#### Comportamental:
* Movimiento irregular (no lineal)
* Intensidad variable
* Acción indirecta
* Persistencia en el tiempo
* Capacidad de transformar sin romper

### Moodboard
<img width="736" height="440" alt="image" src="https://github.com/user-attachments/assets/7b96281d-4513-4d01-a26d-1ccd622a9061" />
<img width="376" height="626" alt="image" src="https://github.com/user-attachments/assets/9dca4dfd-ae4d-44a1-b26f-b6f8caef3827" />
<img width="736" height="1104" alt="image" src="https://github.com/user-attachments/assets/375be8ae-cb7b-4b94-a701-afbcf84a2709" />
<img width="500" height="750" alt="image" src="https://github.com/user-attachments/assets/b0fff736-8ceb-4f4d-b342-b9aadee4a68f" />
<img width="459" height="816" alt="image" src="https://github.com/user-attachments/assets/a580f37d-3652-4984-aaef-a1f0a998b0f3" />


### Bocetos
<img width="1080" height="1045" alt="image" src="https://github.com/user-attachments/assets/5e463215-729b-4d08-9324-264727f13b2c" />
<img width="1600" height="1235" alt="image" src="https://github.com/user-attachments/assets/ffc5bb3b-67e0-4908-969b-490e22f54539" />


### Mapa de decisiones
* Tipografía Helvetica → sensación de claridad y aire
* Espaciado amplio → respiración visual
* Letras como cuerpos físicos independientes → comportamiento orgánico
* Gravedad baja → flotación
* Agua como superficie → Relacion con la marca de agua
* Fricción en el agua → resistencia al movimiento
* Flotación → relación física creíble con el agua
* Audio de viento → activa sistema y genera la brisa
* Noise (Perlin) → evita movimiento mecánico
* Mouse → corrientes de aire

### Mapa de interpretación
#### Inicio
* Palabra quieta
* Sistema en reposo
#### Activación (click → audio)
* El viento comienza
* El agua responde como frenon
#### Desarrollo
* Letras flotan
* Se desplazan suavemente
* El usuario interviene con el mouse

### Relación entre audio y comportamiento
El audio no actúa como un simple detonador de movimiento, sino como un modulador del sistema.
#### El volumen del viento controla:
* Intensidad de las ondas del agua
* Magnitud de las fuerzas aplicadas a las letras
#### La brisa:
* No empuja directamente las letras
* Primero afecta el agua

### Uso de IA
La IA se utilizo para generar el sistema reactivo de las olas y ayudo a mejorar la interactividad del mouse

### Codigo
``` js
const { Engine, World, Bodies, Body } = Matter;

let engine, world;
let letters = [];
let word = "BRISA";

let windSound;
let amplitude;

// agua
let waterPoints = [];
let cols = 120;
let waterLevel;

let started = false;

function preload() {
  soundFormats('mp3', 'wav');
  windSound = loadSound("wind.mp3");
}

function setup() {
  createCanvas(windowWidth, windowHeight);

  engine = Engine.create();
  world = engine.world;
  engine.world.gravity.y = 0;

  textFont('Helvetica');
  textSize(110);
  textAlign(CENTER, CENTER);

  let centerX = width / 2;
  let centerY = height / 2;

  waterLevel = height * 0.80;

  // centrado real
  let totalWidth = textWidth(word);
  let startX = centerX - totalWidth / 2;

  let currentX = startX;

  for (let i = 0; i < word.length; i++) {
    let char = word[i];
    let w = textWidth(char);

    let body = Bodies.rectangle(
      currentX + w / 2,
      centerY + 50,
      w,
      80,
      { frictionAir: 0.02 }
    );

    body.char = char;

    World.add(world, body);
    letters.push(body);

    currentX += w;
  }

  amplitude = new p5.Amplitude();
  amplitude.setInput(windSound);

  for (let i = 0; i < cols; i++) {
    waterPoints.push({
      x: map(i, 0, cols - 1, 0, width),
      baseY: waterLevel,
      offset: random(1000)
    });
  }
}

function draw() {
  background(232, 246, 249);

  Engine.update(engine);

  let level = started ? amplitude.getLevel() : 0.02;
  let wind = map(level, 0, 0.3, 0.0005, 0.002);
  let t = frameCount * 0.01;

  drawWater(level);

  for (let body of letters) {

    // viento
    let nx = noise(body.position.x * 0.005, t);
    let ny = noise(body.position.y * 0.005, t + 100);

    let fx = map(nx, 0, 1, -wind, wind);
    let fy = map(ny, 0, 1, -wind * 0.4, wind * 0.4);

    Body.applyForce(body, body.position, { x: fx, y: fy });

    let waterY = getWaterHeightAt(body.position.x, level);
    let distToWater = body.position.y - waterY;

    if (distToWater > -20 && distToWater < 60) {

      let lift = map(distToWater, -20, 60, 0.004, 0);
      Body.applyForce(body, body.position, { x: 0, y: -lift });

      Body.setVelocity(body, {
        x: body.velocity.x * 0.99,
        y: body.velocity.y * 0.95
      });
    }

    let dx = mouseX - body.position.x;
    let dy = mouseY - body.position.y;
    let d = dist(mouseX, mouseY, body.position.x, body.position.y);

    if (d < 250) {
      let force = map(d, 0, 250, 0.004, 0);

      if (mouseIsPressed) force *= 3;

      Body.applyForce(body, body.position, {
        x: dx * force * 0.001,
        y: dy * force * 0.001
      });
    }

    drawLetter(body);
  }
}

// letras
function drawLetter(body) {
  push();
  translate(body.position.x, body.position.y);
  rotate(body.angle);

  fill(30, 50, 70);
  noStroke();

  text(body.char, 0, 0);
  pop();
}

function drawWater(level) {
  noStroke();
  fill(140, 210, 235, 180);

  beginShape();

  curveVertex(0, getWaterHeightAt(0, level));

  for (let i = 0; i < waterPoints.length; i++) {
    let x = waterPoints[i].x;
    let y = getWaterHeightAt(x, level);

    curveVertex(x, y);
  }

  curveVertex(width, getWaterHeightAt(width, level));

  vertex(width, height);
  vertex(0, height);

  endShape(CLOSE);
}

function getWaterHeightAt(x, level) {
  let i = floor(map(x, 0, width, 0, waterPoints.length - 1));
  let p = waterPoints[i];

  let wave =
    sin(frameCount * 0.015 + p.offset) * 4 +
    sin(frameCount * 0.01 + p.offset * 1.5) * 2;

  let audioWave = level * 40;

  let d = dist(mouseX, mouseY, p.x, p.baseY);
  let mouseInfluence = 0;

  if (d < 150) {
    mouseInfluence = map(d, 0, 150, 25, 0);
  }

  return p.baseY + wave + audioWave - mouseInfluence;
}

function mousePressed() {
  if (!started) {
    userStartAudio();

    windSound.play();
    windSound.setLoop(true);
    windSound.setVolume(1);

    fullscreen(true);

    started = true;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```

### Link del sketch
https://editor.p5js.org/simonburgosb/sketches/gtZ4uLcsN


### Capturas del Trabajo
<img width="928" height="601" alt="image" src="https://github.com/user-attachments/assets/094284ad-d967-49dd-a20b-0a9e668fff24" />
<img width="917" height="655" alt="image" src="https://github.com/user-attachments/assets/5e9828e5-d5ef-464b-9b60-db39aa5dd572" />


## Bitácora de reflexión
