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

## Bitácora de aplicación 



## Bitácora de reflexión
