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



## Bitácora de reflexión
