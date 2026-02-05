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

## Bitácora de reflexión

