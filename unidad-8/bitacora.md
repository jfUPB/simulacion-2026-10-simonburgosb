# Unidad 8

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 
### Herramienta elegida.
La herramienta elegida para el proyecto fue Three.js, una librería de JavaScript enfocada en gráficos 3D interactivos en navegador mediante WebGL.

La elección de esta herramienta responde al interés profesional en experiencias interactivas digitales y desarrollo de videojuegos, especialmente en sistemas físicos en tiempo real e interacción con el usuario. Three.js permite integrar animación, física, interacción y composición visual dentro de una misma experiencia navegable y ejecutable desde web, lo que la convierte en una herramienta pertinente para proyectos de entretenimiento digital e instalaciones interactivas.

### Sistema transferido
El sistema transferido corresponde a un sistema de interacción física basado en Motion 101 pero aplicado a un entorno mas realista como lo seria:
* tensión elástica
* arrastre del mouse
* fuerza acumulada
* liberación de energía cinética

Originalmente, este tipo de sistema fue explorado en p5.js mediante vectores, interacción con mouse y simulaciones físicas simples usando Motion 101. La transferencia consistió en reconstruir ese mismo principio dentro de un entorno 3D usando Three.js y físicas reales.

### Contexto profesional concreto.
La pieza fue pensada como un prototipo interactivo para una experiencia digital orientada al entretenimiento interactivo y videojuegos casuales.

El sistema podría funcionar como:
* minijuego web
* instalación interactiva
* demo de portafolio para diseño interactivo
* experimento de física lúdica

La intención profesional es demostrar capacidades en:
* diseño interactivo
* motion design
* física digital
* programación visual
* interacción en tiempo real

### Concepto visual
“Tensión y liberación”

La pieza explora la acumulación de energía antes del movimiento.

Visualmente, el usuario interactúa con un sistema que responde mediante tensión elástica y liberación cinética, enfatizando principios fundamentales de Motion 101 como anticipación y follow through.

El movimiento no se plantea únicamente como desplazamiento físico, sino como una experiencia visual donde la preparación del movimiento es tan importante como el movimiento mismo.

El uso de una cámara en perspectiva 3/4 permite enfatizar profundidad y sensación espacial.

### Referencias
* Angry Birds
* Wii Sports
* Cut the Rope

### Moodboard
<img width="447" height="314" alt="image" src="https://github.com/user-attachments/assets/fc59c5c8-71c0-489f-bc97-c7c0ad228400" />
<img width="285" height="263" alt="image" src="https://github.com/user-attachments/assets/76d7eab3-0850-491d-bc4e-f66e847f0a13" />
<img width="600" height="450" alt="image" src="https://github.com/user-attachments/assets/5d45c979-95de-43e7-a8c6-acf2023ff893" />
<img width="736" height="559" alt="image" src="https://github.com/user-attachments/assets/4ca4d004-c4cf-468f-8aef-15218482b87f" />

### Explicacion de la transferencia
La transferencia consistió en reinterpretar principios estudiados en Motion 101 dentro de un entorno tridimensional interactivo.

En lugar de trabajar únicamente movimiento gráfico o animación lineal, el proyecto transforma conceptos de:
* tensión
* anticipación
* elasticidad
* reacción
* timing

en un sistema físico manipulable en tiempo real.

La resortera permite visualizar claramente estos principios:
* el estiramiento funciona como anticipación
* la deformación visual representa tensión
* el disparo representa liberación de energía
* el movimiento posterior del proyectil funciona como follow through

### Mapa de decisiones
* Sistema original:
  * Interacción + elasticidad en p5.js
                ↓
* Transferencia:
  * Three.js + Cannon-es
                ↓
* Visualidad:
  * Arcade minimalista 3D
                ↓
* Interacción:
  * Mouse drag + release
                ↓
* Resultado:
  * Experiencia interactiva física

### Mapa de presentacion
* Laptop o monitor
        ↓
* Pantalla completa
        ↓
* Usuario interactúa con mouse
        ↓
* Demostración física en vivo
        ↓
* Explicación del sistema transferido

### Uso de IA
La inteligencia artificial fue utilizada como apoyo técnico para:

* resolución de errores
* mejora en la integración de físicas
* optimización de interacción


### Codigos Fuentes 
#### Control
``` js
import * as THREE from 'three'

export const scene = new THREE.Scene()

scene.background = new THREE.Color(0x87ceeb)

export const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
)

// Cámara 3/4
camera.position.set(8, 6, 10)
camera.lookAt(0, 2, 0)

export const renderer = new THREE.WebGLRenderer({
  antialias: true
})

renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)


// Luces
const ambient = new THREE.AmbientLight(0xffffff, 0.7)
scene.add(ambient)

const directional = new THREE.DirectionalLight(0xffffff, 1)
directional.position.set(5, 10, 5)

scene.add(directional)


// Piso
const floorGeo = new THREE.PlaneGeometry(50, 50)

const floorMat = new THREE.MeshStandardMaterial({
  color: 0x228B22
})

const floor = new THREE.Mesh(floorGeo, floorMat)

floor.rotation.x = -Math.PI / 2

scene.add(floor)


// Resize
window.addEventListener('resize', () => {

  camera.aspect = window.innerWidth / window.innerHeight

  camera.updateProjectionMatrix()

  renderer.setSize(window.innerWidth, window.innerHeight)

})
```

#### Physics
``` js
import * as CANNON from 'cannon-es'

export const world = new CANNON.World()

world.gravity.set(0,-9.82,0)


// Piso físico
const floorBody = new CANNON.Body({
  type:CANNON.Body.STATIC,
  shape:new CANNON.Plane()
})

floorBody.quaternion.setFromEuler(-Math.PI/2,0,0)

world.addBody(floorBody)
```


#### Scene
``` js
import * as THREE from 'three'

export const scene = new THREE.Scene()

scene.background = new THREE.Color(0x87ceeb)

export const camera = new THREE.PerspectiveCamera(
  75,
  window.innerWidth / window.innerHeight,
  0.1,
  1000
)

// Cámara 3/4
camera.position.set(8, 6, 10)
camera.lookAt(0, 2, 0)

export const renderer = new THREE.WebGLRenderer({
  antialias: true
})

renderer.setSize(window.innerWidth, window.innerHeight)
document.body.appendChild(renderer.domElement)


// Luces
const ambient = new THREE.AmbientLight(0xffffff, 0.7)
scene.add(ambient)

const directional = new THREE.DirectionalLight(0xffffff, 1)
directional.position.set(5, 10, 5)

scene.add(directional)


// Piso
const floorGeo = new THREE.PlaneGeometry(50, 50)

const floorMat = new THREE.MeshStandardMaterial({
  color: 0x228B22
})

const floor = new THREE.Mesh(floorGeo, floorMat)

floor.rotation.x = -Math.PI / 2

scene.add(floor)


// Resize
window.addEventListener('resize', () => {

  camera.aspect = window.innerWidth / window.innerHeight

  camera.updateProjectionMatrix()

  renderer.setSize(window.innerWidth, window.innerHeight)

})
```
#### Slingshot 
``` js
import * as THREE from 'three'

import * as CANNON from 'cannon-es'

import { scene } from './scene'

import { world } from './physics'


export let projectileMesh
export let projectileBody

const leftAnchor = new THREE.Vector3(-1, 2, 0)

const rightAnchor = new THREE.Vector3(1, 2, 0)

const restPoint = new THREE.Vector3(0, 2, 0)


// Material madera
const woodMat = new THREE.MeshStandardMaterial({
  color: 0x8B4513
})


// Postes
const poleGeo = new THREE.BoxGeometry(0.3, 4, 0.3)

const leftPole = new THREE.Mesh(poleGeo, woodMat)

leftPole.position.set(-1, 2, 0)

scene.add(leftPole)

const rightPole = new THREE.Mesh(poleGeo, woodMat)

rightPole.position.set(1, 2, 0)

scene.add(rightPole)


// Proyectil
const sphereGeo = new THREE.SphereGeometry(0.4, 32, 32)

const sphereMat = new THREE.MeshStandardMaterial({
  color: 0xff4444
})

projectileMesh = new THREE.Mesh(
  sphereGeo,
  sphereMat
)

projectileMesh.position.set(0, 2, 0)

scene.add(projectileMesh)


// Física proyectil
projectileBody = new CANNON.Body({
  mass: 1,
  shape: new CANNON.Sphere(0.4),
  position: new CANNON.Vec3(0, 2, 0)
})

world.addBody(projectileBody)


// Material bandas
const bandMat = new THREE.LineBasicMaterial({
  color: 0x552200
})


// Geometrías iniciales
const geo1 = new THREE.BufferGeometry().setFromPoints([
  leftAnchor,
  projectileMesh.position
])

const geo2 = new THREE.BufferGeometry().setFromPoints([
  rightAnchor,
  projectileMesh.position
])


// Líneas
export const band1 = new THREE.Line(
  geo1,
  bandMat
)

export const band2 = new THREE.Line(
  geo2,
  bandMat
)

scene.add(band1)

scene.add(band2)


// Actualizar bandas
export function updateBands() {

  const target = projectileBody.type === 4
    ? projectileMesh.position
    : restPoint

  band1.geometry.setFromPoints([
    leftAnchor,
    target
  ])

  band2.geometry.setFromPoints([
    rightAnchor,
    target
  ])
}
```
#### Main
``` js
import { scene, camera, renderer } from './scene'

import { world } from './physics'

import {
  projectileMesh,
  projectileBody,
  updateBands
} from './slingshot'

import './control'


function animate() {

  requestAnimationFrame(animate)

  // Física
  world.fixedStep()

  // SOLO sincronizar cuando es dinámico
  if (projectileBody.type === 1) {

    projectileMesh.position.copy(
      projectileBody.position
    )

    projectileMesh.quaternion.copy(
      projectileBody.quaternion
    )
  }

  updateBands()

  renderer.render(
    scene,
    camera
  )
}

animate()
```

### Registro visual
<img width="1908" height="852" alt="image" src="https://github.com/user-attachments/assets/907d33b6-879b-4154-abc3-b37fc9add16b" />


## Bitácora de reflexión
