<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>💖EN SERIO ME ENCANTAS, TE AMO💖</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.6.0/p5.min.js"></script>
  <style>
    body {
      margin: 0;
      background: black;
      overflow: hidden;
    }
    h1 {
      position: absolute;
      top: 20px;
      width: 100%;
      text-align: center;
      font-size: 2.5em;
      font-family: "Courier New", monospace;
      color: white;
      text-shadow:
        0 0 5px #ff33cc,
        0 0 10px #ff33cc,
        0 0 20px #ff33cc,
        0 0 40px #ff33cc;
    }
  </style>
</head>
<body>
  <h1>💖😍 PARA LA NIÑA MAS HERMOSA QUE HE VISTO 😍💖</h1>
  <script>
    let flowers = [];
    let butterflies = [];

    function setup() {
      createCanvas(windowWidth, windowHeight);

      // Crear girasoles dispersos
      for (let i = 0; i < 30; i++) {
        let x = random(50, width - 50);
        let y = random(100, height - 50);
        flowers.push(new Flower(x, y));
      }

      // Crear mariposas
      for (let i = 0; i < 10; i++) {
        butterflies.push(new Butterfly());
      }
    }

    function draw() {
      background(0); // negro sólido

      // Dibujar flores
      for (let f of flowers) {
        f.update();
        f.show();
      }

      // Dibujar mariposas
      for (let b of butterflies) {
        b.update();
        b.show();
      }
    }

    class Flower {
      constructor(x, y) {
        this.x = x;
        this.y = y;
        this.size = random(30, 50);
        this.petals = int(random(20, 25));
        this.angle = random(TWO_PI);
      }

      update() {
        this.angle += 0.002;
      }

      show() {
        push();
        translate(this.x, this.y);
        rotate(this.angle);

        // pétalos con brillo suave
        for (let i = 0; i < this.petals; i++) {
          let angle = TWO_PI / this.petals * i;
          let px = cos(angle) * this.size;
          let py = sin(angle) * this.size;
          let r = map(i, 0, this.petals, 200, 255); // degradado radial en amarillo
          fill(r, 180 + r * 0.1, 0, 220);
          noStroke();
          ellipse(px, py, this.size / 3, this.size);
        }

        // centro marrón con brillo
        for (let r = this.size; r > 0; r -= 2) {
          fill(150 + r * 0.3, 80 + r * 0.2, 30, 200);
          ellipse(0, 0, r, r);
        }

        pop();
      }
    }

    class Butterfly {
      constructor() {
        this.reset();
      }

      reset() {
        this.x = random(width);
        this.y = random(height / 2, height - 100);
        this.size = random(15, 25);
        this.speedX = random(-1, 1);
        this.speedY = random(-0.5, 0.5);
        this.opacity = random(180, 255);
        this.lifetime = int(random(200, 400));
        this.color = [random(150, 255), random(100, 200), random(200, 255)];
      }

      update() {
        this.x += this.speedX;
        this.y += this.speedY;
        this.lifetime--;

        if (this.lifetime <= 0 || this.x < 0 || this.x > width || this.y < 50 || this.y > height - 50) {
          this.reset();
        }
      }

      show() {
        push();
        translate(this.x, this.y);
        rotate(sin(frameCount * 0.1));
        noStroke();
        fill(this.color[0], this.color[1], this.color[2], this.opacity);
        ellipse(-this.size / 2, 0, this.size, this.size / 2);
        ellipse(this.size / 2, 0, this.size, this.size / 2);
        pop();
      }
    }

    function windowResized() {
      resizeCanvas(windowWidth, windowHeight);
    }
  </script>
</body>
</html>
