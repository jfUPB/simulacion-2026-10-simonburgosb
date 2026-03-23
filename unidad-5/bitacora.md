# Unidad 5
## Bitácora de proceso de aprendizaje

## ACTIVIDAD 1

### ¿Qué propiedades tiene cada partícula?

Estado físico:
* position (posición)
* velocity (velocidad)
* acceleration (aceleración)


Estado vital:
* lifespan (tiempo de vida)

### ¿Qué condición determina que una partícula muere?
isDead() {
  return this.lifespan < 0;
}

### ¿Cómo se actualiza la partícula? (Motion 101)
* velocity.add(acceleration);
* position.add(velocity);
* acceleration.mult(0);
* lifespan -= 2;

### ¿Quién crea las partículas?

En tu código original:
* particles.push(new Particle(width / 2, 20));

En la versión con Emitter:
* this.particles.push(new Particle());

### ¿En qué momento se crean?
En cada frame (draw())


### ¿Quién decide cuándo eliminar una partícula?

El Emitter con:
if (particle.isDead()) {
  particles.splice(i, 1);
}

### ¿Por qué recorrer el array en orden inverso?
for (let i = particles.length - 1; i >= 0; i--)


### ¿Qué pasa si nunca eliminas partículas?
* El array crece infinitamente
* Más partículas → más cálculos
* Más memoria usada
* FPS ↓↓↓↓↓

### ¿Cómo se representa una partícula?

fill(0, lifespan);
ellipse(position.x, position.y, 8, 8);

### Si quisiera usar líneas en vez de círculos…

line(this.position.x, this.position.y,
     this.position.x + 10, this.position.y);


## ACTIVIDAD 2
### ¿Qué responsabilidades que antes estaban en draw() ahora están en Emitter?

Antes en draw() tenías:

* Crear partículas (push)
* Recorrer el array
* Actualizar cada partícula
* Dibujarlas
* Eliminar las muertas

Ahora todo eso vive dentro de:

* emitter.run();
* emitter.addParticle();

### ¿Ventaja de encapsular en una clase Emitter?

1. Organización
* Ya no tienes lógica mezclada en draw()
* Cada cosa tiene su rol claro

2. Reutilización
Puedes crear múltiples emisores fácilmente

3. Escalabilidad
* Puedes agregar comportamientos distintos por emisor
* fuego
* humo 
* explosión 

4. Abstracción
* No piensas en partículas individuales
* Piensas en sistemas completos

### ¿Quién crea los emitters y quién crea las partículas?

* Emitters:

function mousePressed() {
  emitters.push(new Emitter(mouseX, mouseY));
}

* Partículas:

emitter.addParticle();
### Transferencia de conceptos
Se tiene un sistema compuesto por múltiples emisores. Cada emisor es una entidad que administra una colección de partículas. Cada partícula posee un estado físico, definido por su posición, velocidad y aceleración, y un estado vital, representado por su tiempo de vida.

En cada ciclo del sistema:

* Los emisores generan nuevas partículas en su posición de origen.
* A cada partícula se le aplican fuerzas externas (como la gravedad), que modifican su movimiento.
* Las partículas actualizan su estado físico en función de estas fuerzas.
* Paralelamente, su estado vital disminuye progresivamente.


## Actividad 3

### ¿Qué tienen en común las subclases de partículas? ¿Qué tienen de diferente?

Todas las partículas comparten:

#### Estado físico
* posición
* velocidad
* aceleración
#### Estado vital
* lifespan
#### Comportamientos base
* applyForce()
* update()
* isDead()


### ¿Por qué el Emitter no necesita saber el tipo de partícula?
El emisor trabaja con una interfaz común, no con tipos específicos.


### Si agregas un tercer tipo de partícula…
Tienes que crear:

* Una nueva clase, por ejemplo:

class ParticleFire extends Particle {
  show() {
    fill(255, 100, 0, this.lifespan);
    circle(this.position.x, this.position.y, 10);
  }
}


### Comparación con Example 4.2

* No cambia el emitter ni la muerte de las partciulas

¿Qué capa cambió?

* Capa de comportamiento / visualización de la partícula

  * Nuevos estilos
  * Nuevas formas
  * Nuevas dinámicas



## Bitácora de aplicación 


## Bitácora de reflexión
