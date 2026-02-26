# Unidad 1

## Bitácora de proceso de aprendizaje
### Actividad 1
La aleatoriedad en el arte generativo actúa como una chispa de imprevisibilidad que rompe el control total del creador y permite que emerjan formas, patrones y significados inesperados que hacen cada obra única.
### Actividad 2 
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;
let num;

function setup() {
  createCanvas(640, 240);
  walker = new Walker(); //Guarda la direccion del objeti tipo waker creando una nueva funcion
  background(255);
  num = floor(random(2));
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    if (num == 0) {
    stroke(0);
    point(this.x, this.y);
    }else if (num == 1) {
   stroke(0);
  circle(this.x, this.y, 50);
    }
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x--;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

espero que salga un circulo ya que tiene un 50% de probabilidad de salir. Efectivamente despues de probar salio el circulo. Lo essperaba ya que tiene una probabilidad de la mitad. 

### Actividad 3
Una distribucion uniforme es dodne los valores tienen la msima distancia unos de otros y no hay una variacion entre ellos; mientras que una no uniforme permite mas disprecion de datos. 
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;
let num;

function setup() {
  createCanvas(640, 240);
  walker = new Walker(); //Guarda la direccion del objeti tipo waker creando una nueva funcion
  background(255);
  num = floor(random(2));
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
  }

  show() {
    if (num == 0) {
    stroke(0);
    point(this.x, this.y);
    }else if (num == 1) {
   stroke(0);
  circle(this.x, this.y, 50);
    }
  }

  step() {
    const choice = floor(random(4));
    if (choice == 0) {
      this.x++;
    } else if (choice == 1) {
      this.x++;
    } else if (choice == 2) {
      this.y++;
    } else {
      this.y--;
    }
  }
}
```

### Actividad 4 

``` js
function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  //{!1} A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 60);
  let y = randomGaussian(120, 40);
  noStroke();
  fill(0, 10);
  circle(x, y, 16);
```

[Archivo p5.js](https://editor.p5js.org/simonburgosb/sketches/BeVWAln3C)

![Img Actividad](actividad4.png)

### Actividad 5 
Use esta tecnica para hacer como un salto de movimiento
``` js
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;
let num;

function setup() {
  createCanvas(640, 240);
  walker = new Walker(); //Guarda la direccion del objeti tipo waker creando una nueva funcion
  background(255);
  num = floor(random(2));
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width/2 ;
    this.y = height/2 ;
  }

  show() {
    if (num == 0) {
    stroke(0);
    point(this.x, this.y);
    }else if (num == 1) {
   stroke(0);
  circle(this.x, this.y, 50);
    }
  }

  step() {
    let r = random(1);
    let xStep;
    let yStep;
//{!3} A 1% chance of taking a large step
if (r < 0.01) {
  xStep = random(-100, 100);
  yStep = random(-100, 100);
} else {
  xStep = random(-1, 1);
  yStep = random(-1, 1);
}
    
    this.x += xStep;
    this.y += yStep
  }
}

```

[Archivo p5.js](https://editor.p5js.org/simonburgosb/sketches/UJ_XaLKmO)
![Img Actividad](actividad5.png)

### Actividad 6

Espero que cuando incie el programa pase que durante el ancho de la pantalla se vaya proyectando el ruido de perlin en forma de grafico
``` js
let xoff = 0;

function setup() {
  createCanvas(600, 400);
  background(255);
}

function draw() {
  stroke(0);

  let x = 0;
  xoff = 0;

  while (x < width) {
    let y = noise(xoff) * height;
    line(x, height, x, height - y);

    xoff += 0.02;
    x += 10;
  }
}


```
([https://editor.p5js.org/simonburgosb/sketches/otxT05gaM])
![Img Actividad](actividad6.png)
## Bitácora de aplicación 
Este diseño genera una composición interactiva donde, al hacer clic, se selecciona aleatoriamente una forma geométrica y esta se dibuja repetidamente en posiciones que varían según una distribución normal, haciendo que la mayoría de las apariciones se concentren cerca del centro del lienzo; al mismo tiempo, el color de relleno cambia de manera suave usando ruido Perlin

``` js
let particula;
let f;

function setup() {
  createCanvas(600, 600);
  particula = new Particula();
}

function draw() {
  background(220);

  particula.forma = f;
  particula.move();
  particula.form();
}

function mousePressed() {
  f = int(random(1, 4));
}

class Particula {
  constructor() {
    // centro base
    this.cx = width / 2;
    this.cy = height / 2;

    this.x = this.cx;
    this.y = this.cy;

    this.tc = random(1000); // noise para color
    this.forma = 1;
  }

  move() {
    // movimiento con distribución normal
    this.x = randomGaussian(this.cx, 20);
    this.y = randomGaussian(this.cy, 20);
  }

  form() {
    // fill controlado por noise
    let c = noise(this.tc) * 255;
    fill(c, 150, 200);
    noStroke();
    this.tc += 0.01;

    if (this.forma === 1) {
      circle(this.x, this.y, 30);
    } 
    else if (this.forma === 2) {
      rect(this.x, this.y, 30, 30);
    } 
    else if (this.forma === 3) {
      triangle(
        this.x, this.y - 15,
        this.x - 15, this.y + 15,
        this.x + 15, this.y + 15
      );
    }
  }
}

```
([https://editor.p5js.org/simonburgosb/sketches/O_0apqmVL])
![Img Actividad](actividad7.png)


## Bitácora de reflexión

### 1. Diferencia entre random() y Ruido Perlin (noise())

La diferencia fundamental es que **random() genera valores completamente independientes**, es decir, cada número es impredecible y no tiene relación con el anterior. Esto produce cambios bruscos y resultados más caóticos.  

En cambio, el Ruido Perlin (**noise()**) genera valores que cambian de forma **suave y continua**, porque los valores cercanos están correlacionados. Por eso, aunque parece aleatorio, tiene una estructura interna.

- **Usaría random()** cuando quiero saltos inesperados, como escoger una forma al azar o hacer partículas explosivas.  
- **Usaría noise()** cuando busco variaciones orgánicas, como movimientos fluidos, texturas naturales o cambios graduales de color.

### 2. Distribución de probabilidad y diferencia visual entre uniforme y normal

Una **distribución de probabilidad** es una forma de describir qué tan probable es que aparezcan ciertos valores dentro de un rango. No todos los números tienen por qué ocurrir con la misma frecuencia: algunos pueden ser más comunes y otros más raros.

En una caminata aleatoria con **distribución uniforme**, todos los pasos tienen la misma probabilidad, lo que genera trayectorias más dispersas y erráticas.  

En una caminata con **distribución normal (Gaussian)**, la mayoría de los pasos son pequeños y se concentran alrededor de un valor promedio, produciendo un movimiento más suave, natural y agrupado.

Visualmente:

- Uniforme → más caótica  
- Normal → más orgánica  

### 3. Papel de la aleatoriedad en el arte generativo

La aleatoriedad cumple varias funciones importantes en el arte generativo:

1. **Generar variación y sorpresa**, evitando que cada obra sea idéntica o totalmente predecible.  
2. **Simular comportamientos naturales**, como crecimiento, movimiento orgánico o irregularidades presentes en el mundo real.  

Además, permite que el artista diseñe sistemas abiertos donde el resultado final emerge del proceso.

### 4. Concepto usado en tu obra final (Actividad 07)

En mi obra final utilicé el concepto de **randomGaussian** para controlar la posición de las formas y los colores se modifican levemente con noise. 

Esto generó una composición equilibrada: no totalmente uniforme ni completamente caótica. El efecto buscado era que las formas parecieran surgir de manera orgánica, como si existiera un patrón al azar.

### 5. ¿Qué es una caminata (walk) en simulación? ¿Qué es un Lévy flight?

Un “paseo” o “caminata” (**random walk**) es un proceso donde un objeto se mueve paso a paso tomando decisiones aleatorias en cada iteración.

Una caminata tipo **Lévy flight** se caracteriza porque combina muchos pasos pequeños con saltos largos ocasionales. 

Es común en fenómenos como la búsqueda de comida en animales o ciertos patrones de exploración.
