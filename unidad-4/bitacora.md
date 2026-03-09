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



## Bitácora de reflexión

