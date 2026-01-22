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

[Archivo p5.js](https://ejemplo.com)

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

[Archivo p5.js]([https://ejemplo.com](https://editor.p5js.org/simonburgosb/sketches/UJ_XaLKmO))

## Bitácora de aplicación 



## Bitácora de reflexión


