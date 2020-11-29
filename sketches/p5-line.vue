<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/p5.min.js"></script>

<script lang="ts">
/// <reference path="../node_modules/@types/p5/global.d.ts" />

let dim = 0

let waves = 256
let waveAngles = []
let currAngle = 0
let innerR

let delta = 0

let c1
let c2

function setup() {
  dim = min(windowWidth, windowHeight) * 0.8
  innerR = dim / 10

  createCanvas(dim, dim)
  background(255)

  c1 = color('#64BCAD')
  c1.setAlpha(100)
  c2 = color('#74CCFF')

  currAngle = atan2(mouseY - dim / 2, mouseX - dim / 2)
  waveAngles = []
  for (let i = 0; i < waves + 1; i++) {
    waveAngles.push(currAngle + (TWO_PI / waves) * i)
  }
}

function draw() {
  background(255)

  for (let i = 0; i < waveAngles.length; i++) {
    const a = waveAngles[i]
    const b = waveAngles[(i + delta) % waveAngles.length]

    stroke(lerpColor(c1, c2, i / waveAngles.length))
    line(
      dim / 2 + (cos(a) * innerR) / map(a, currAngle, currAngle + PI, 0.2 * PI, PI * 0.8),
      dim / 2 + sin(a) * innerR * map(a - currAngle, 0, TWO_PI, 4, 1),
      dim / 2 + cos(b) * innerR * map(b - currAngle, 0, TWO_PI, 4, 1),
      dim / 2 + (sin(b) * innerR) / map(b, currAngle, currAngle + PI, 0.2 * PI, PI * 0.8)
    )
  }

  delta++
}

function mouseMoved() {
  currAngle = atan2(mouseY - dim / 2, mouseX - dim / 2)
  waveAngles = []
  for (let i = 0; i < waves + 1; i++) {
    waveAngles.push(currAngle + (TWO_PI / waves) * i)
  }
}
</script>

<style>
div {
  font-size: 4rem;
  margin-bottom: 2rem;
}
body {
  margin: 0;
  display: flex;

  height: 100vh;
  width: 100vw;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
}
pre {
  position: fixed;
  color: rgba(40, 40, 40, 0.8);
}
</style>