# Unidad 4

## Bitácora de proceso de aprendizaje

### Actividad 1
Uno de los aspectos que más me llamó la atención de la obra Simple Harmonic Motion de Memo Akten es la manera en que combina arte, matemáticas y tecnología para crear experiencias audiovisuales complejas a partir de reglas muy simples. La obra investiga cómo comportamientos complejos pueden surgir de la interacción entre patrones simples repetitivos.

### Actividad 2
En esta simulación se observa un objeto formado por una línea y dos círculos que rota continuamente alrededor de un punto central. La interacción principal consiste en visualizar cómo funciona la rotación en un sistema de coordenadas y cómo el ángulo va cambiando frame a frame para generar movimiento. La función rotate() aplica una rotación al sistema de coordenadas. Esto significa que no rota únicamente el objeto, sino que todo lo que se dibuje después se verá afectado por esa rotación.
Estos componentes indican la dirección del movimiento. La función heading() convierte ese vector en un ángulo de rotación.

El proceso completo es:
* El objeto se mueve usando su vector de velocidad.
* Se calcula el ángulo del vector con heading().
* Se traslada el sistema de coordenadas a la posición del objeto con translate().
* Se rota el sistema con rotate(angle).
* Se dibuja el objeto centrado en (0,0).

Funciones push() y pop()
* push() guarda el estado actual del sistema de transformaciones (traslación, rotación, escala, etc.).
* pop() restaura ese estado guardado.
Esto sirve para que las transformaciones aplicadas dentro del bloque no afecten a otros objetos que se dibujen después.

### Actividad 3
Se utilizaron transformaciones del sistema de coordenadas, como translate() y rotate(), para posicionar y orientar el vehículo correctamente. La orientación del vehículo se calcula a partir del vector de velocidad usando la función heading(), lo que permite que el triángulo siempre apunte hacia la dirección en la que se está moviendo.

### Actividad 4
#### Modificación necesaria para usar fuerzas acumulativas
Cuando se utilizan fuerzas acumulativas, es necesario reiniciar la aceleración después de cada actualización. Esto se hace con la línea: this.acceleration.mult(0);

#### Uso de dragging y rollover

Los atributos:
* this.dragging
* this.rollover
permiten crear interacción con el mouse.

* dragging: indica si el attractor está siendo arrastrado.
* rollover: indica si el mouse está encima del attractor.
Para que funcionen, se pueden usar las funciones de p5.js:
* mousePressed()
* mouseReleased()
* mouseDragged()

### Actividad 5
Las coordenadas polares se definen mediante dos valores:
* r (radio): la distancia desde el origen hasta el punto.
* theta (θ): el ángulo que forma el punto con respecto al eje horizontal.

Para convertir estas coordenadas polares a coordenadas cartesianas se utilizan las siguientes fórmulas:
* x=r⋅cos(θ)
* y=r⋅sin(θ)

#### Primer resultado
En este caso ocurre un problema porque las variables x y y no están definidas dentro del código. La función line(0,0,x,y) intenta dibujar una línea hacia un punto (x,y) que no existe, lo que genera un error o hace que la línea no se dibuje correctamente.

#### Segundo resultado
En este caso la simulación funciona correctamente porque:
* El vector ahora se crea con ángulo (theta) y magnitud (r).
* Esto genera un vector cuyo tamaño corresponde al valor de r.


### Actividad 6
Este ejercicio me permitió entender cómo las funciones sinusoides se utilizan para generar movimientos suaves y periódicos en programación creativa. También pude observar cómo pequeños cambios en los parámetros modifican significativamente el comportamiento de la onda. Estos conceptos son fundamentales para crear animaciones naturales, simulaciones físicas y patrones visuales en proyectos de arte generativo e interacción.


### Actividad 7
Este ejercicio me permitió combinar conceptos de diferentes unidades del curso. Por un lado, el uso de ruido de Perlin introduce variación controlada en el sistema, mientras que el uso de fuerzas permite modificar el comportamiento dinámico de los osciladores. La combinación de ambos conceptos demuestra cómo pequeños cambios en el modelo matemático pueden producir resultados visuales mucho más complejos e interesantes en simulaciones generativas.

### Actividad 8
Este ejercicio me ayudó a comprender cómo las funciones sinusoidales pueden utilizarse para crear movimientos periódicos en animaciones. También reforzó la importancia de actualizar variables dentro de draw() para producir movimiento continuo. Pequeños cambios en parámetros como la amplitud, la velocidad angular o el ángulo inicial pueden modificar significativamente el comportamiento visual de la onda.

### Actividad 9
Este ejercicio permitió comprender mejor cómo funcionan los sistemas físicos compuestos por múltiples fuerzas interconectadas. Al agregar un segundo resorte, el sistema se vuelve más dinámico porque cada objeto afecta el movimiento del otro. Esto demuestra cómo pequeñas modificaciones en un sistema físico pueden generar comportamientos más complejos en simulaciones interactivas.

### Actividad 10
Este ejercicio permitió comprender cómo los sistemas físicos pueden volverse más complejos al conectar varios elementos entre sí. Un sistema de péndulos en serie genera movimientos más dinámicos e impredecibles que un péndulo simple. También ayudó a reforzar el uso de vectores, ángulos y aceleración angular para simular fenómenos físicos dentro de una animación interactiva.

## Bitácora de aplicación 
La obra imagina un ecosistema de datos que ha sobrevivido a un sistema operativo obsoleto. Estos péndulos no son objetos físicos, sino "procesos" que intentan  apegarse a la realidad para mantenerse organizados. Sin embargo, el sistema está degradado, lo que genera ruido y fallos visuales.

``` js

let pendulums = [];
let num = 25;

function setup() {
  createCanvas(windowWidth, windowHeight);
  // Creamos varios péndulos con diferentes longitudes
  for (let i = 0; i < num; i++) {
    pendulums.push(new Pendulum(width / 2, 50, 150 + (i * 15)));
  }
}

function draw() {
  // Estética teamLab: Estela de luz
  background(0, 30); 
  
  for (let p of pendulums) {
    // --- UNIDAD 3: FUERZAS ---
    
    // 1. Fuerza de Gravedad (Simplificada para péndulo: -g * sin(theta))
    let gravity = 0.8;
    let forceMagnitude = -1 * gravity * sin(p.angle);
    
    // 2. Unidad 1: Ruido de Perlin (Viento digital)
    let n = noise(p.noiseOffset, frameCount * 0.01);
    let wind = map(n, 0, 1, -0.05, 0.05);

    // Aplicamos las fuerzas al sistema
    p.applyForce(forceMagnitude);
    p.applyForce(wind);
    
    // Interactividad: Mouse afecta la aceleración angular
    if (mouseIsPressed) {
      let mouseForce = map(mouseX - pmouseX, -20, 20, -0.02, 0.02);
      p.applyForce(mouseForce);
    }

    // --- UNIDAD 2: MOTION 101 ---
    p.update();
    p.display();
  }
}

class Pendulum {
  constructor(x, y, r) {
    this.origin = createVector(x, y);
    this.position = createVector(0, 0);
    this.r = r;
    this.angle = PI / 4;
    
    this.velocity = 0.0;
    this.acceleration = 0.0;
    this.damping = 0.992; // Resistencia del aire
    this.noiseOffset = random(1000);
  }

  // Método requerido por la Unidad 3
  applyForce(f) {
    // Asumimos masa 1, entonces F = A
    this.acceleration += f / (this.r * 0.1); // La longitud afecta la aceleración
  }

  update() {
    // Lógica Motion 101 aplicada a rotación
    this.velocity += this.acceleration;
    this.velocity *= this.damping;
    this.angle += this.velocity;

    // Conversión a coordenadas cartesianas para dibujo (Vectores)
    this.position.set(this.r * sin(this.angle), this.r * cos(this.angle));
    this.position.add(this.origin);

    // REGLA DE ORO: Limpiar aceleración (Unidad 3)
    this.acceleration = 0;
    this.noiseOffset += 0.01;
  }

  display() {
    stroke(255, 50);
    strokeWeight(1);
    
    // Brazo del péndulo (Estética Ikeda)
    line(this.origin.x, this.origin.y, this.position.x, this.position.y);
    
    // El "punto" de datos
    fill(255);
    noStroke();
    rectMode(CENTER);
    
    // Glitch visual aleatorio tipo Ikeda
    if (random(1) > 0.98) {
      rect(this.position.x, this.position.y, random(20, 100), 1);
      textSize(8);
      text("DATA_STRM_" + floor(this.position.y), this.position.x + 10, this.position.y);
    }
    
    ellipse(this.position.x, this.position.y, 4, 4);
  }
}
```
https://editor.p5js.org/simonburgosb/sketches/zh2frZAi2


<img width="926" height="681" alt="image" src="https://github.com/user-attachments/assets/65de54c3-2152-46e1-9365-1342b9018af8" />

<img width="911" height="677" alt="image" src="https://github.com/user-attachments/assets/bc2c450b-ad15-4692-9c5d-0b62e2c3444e" />


## Bitácora de reflexión

<img width="1278" height="655" alt="image" src="https://github.com/user-attachments/assets/2822ab37-a515-4ba7-8d17-1d9af9a636cc" />

1. Visualización de Datos Dinámica (Data Viz)
* Oportunidad: Olvidar los gráficos estáticos de Excel.
* Aplicación: Usar la Unidad 2 (Motion) y Unidad 3 (Fuerzas) para crear tableros donde los datos económicos o métricas de usuario se comporten como organismos vivos. Si una métrica cae, la "gravedad" vectorial la arrastra; si hay volatilidad, el Ruido de Perlin (Unidad 1) agita los nodos.

2. Diseño de Interfaces (UI/UX) Generativo
* Oportunidad: Crear experiencias de usuario que no se sientan rígidas ni predecibles.
* Aplicación: Aplicar Fuerzas de Atracción y Repulsión en menús interactivos. En lugar de animaciones lineales, usar sistemas donde los elementos de la interfaz orbiten el cursor del usuario, creando una sensación de "fluidez orgánica" que mejora el engagement.

3. Instalaciones Inmersivas y "Phygital"
* Oportunidad: Espacios físicos que reaccionan a las personas (estilo teamLab).
* Aplicación: Integrar sensores (cámara, Kinect, micrófonos) como entradas de fuerza externas. Tu perfil profesional gana un diferencial enorme al poder proponer espacios donde las paredes "cobran vida" usando Sistemas de Partículas (Unidad 4) que huyen o siguen a los clientes en una tienda o galería.

4. Simulación y Prototipado
* Oportunidad: Modelar comportamientos del mundo real sin software de ingeniería pesado.
* Aplicación: Usar la lógica de Vectores y Masas para simular flujos de personas, logística de almacenes o incluso comportamientos de fluidos de manera visual y rápida para presentaciones de alto impacto.


