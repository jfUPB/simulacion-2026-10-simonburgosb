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

## Actividad 4
### Ejemplo 4.6
### ¿Dónde se define la gravedad?
let gravity = createVector(0, 0.1);
### ¿Quién la aplica a las partículas?
emitter.applyForce(gravity);

Es una fuerza global

### Example 4.7

### Que diferencia las fuerzas
| Fuerza   | Tipo      | Cómo se calcula      |
| -------- | --------- | -------------------- |
| Gravedad | Constante | Igual para todas     |
| Repeller | Variable  | Depende de distancia |

### ¿Dónde “vive” cada una?

Gravedad
* Vive en draw()
* Es externa al sistema
Repeller
* Vive en su propia clase Repeller
* Tiene lógica propia (repel())

### ¿Qué principio físico se modela?
Ley del inverso del cuadrado de la distancia

### ¿Cambió la clase Particle?

Prácticamente no por lo cual la partícula no sabe qué fuerzas existen

### MODIFICACIÓN

Voy a elegir:

(b) Cambiar las fuerzas sin cambiar estructura ni visualización
Modificación: agregar viento lateral
Cambio realizado

En draw() agregué:
* let wind = createVector(0.05, 0);
* emitter.applyForce(wind);

### ¿Qué clases/funciones modifiqué?

* Ninguna clase existente
* Solo agregué lógica en draw()

### ¿Qué NO modifiqué?
* Particle
* Emitter
* Repeller
* show()
* isDead()

### ¿Por qué fue posible?

Porque el sistema está diseñado así para que las fuerzas sean externas y desacopladas

| Aspecto                               | 4.2                   | 4.4       | 4.5                      | 4.6                    | 4.7                        |
| ------------------------------------- | --------------------- | --------- | -------------------------| ---------------------- | ---------------------------|
| **¿Quién crea partículas?**           | draw() directamente | Emitter     |Emitter                   |Emitter                 | Emitter                    |
| **¿Hay clase Emitter?**               |  No                 |  Sí         | Sí                       | Sí                     | Sí                         |
| **¿Hay herencia?**                    | No                  | No          | Sí                       | No                     | No                         |
| **¿Hay fuerzas externas?**            |  No                 | No          |  No                      | Sí (gravedad)          | Sí (gravedad + repeller)   |
| **¿Hay interacción entre elementos?** | No                  |  No         |  No                      | No (solo fuerza global)| Sí (repeller ↔             |
| **¿Cómo mueren las partículas?**      | Por lifespan < 0    | Igual       | Igual                    | Igual                  | Igual                      |

## Bitácora de aplicación 
Busca comunicar cómo las ideas pueden crecer y conectarse, pero también cómo pierden fuerza con el tiempo hasta desaparecer. La interacción del usuario simboliza el acto de generar nuevas ideas como impulsos individuales y de momentos ya que no es constante y alimentar el sistema.

<img width="1600" height="639" alt="image" src="https://github.com/user-attachments/assets/f0dda5ba-f92e-4149-98d0-8bfe080b6d99" />


## Bitácora de reflexión
