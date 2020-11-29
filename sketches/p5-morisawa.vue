<script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.1.9/p5.min.js"></script>

<script lang="ts">
/// <reference path="../node_modules/@types/p5/global.d.ts" />
import p5 from 'p5'

let running = true
let loc: p5.Vector
let velocity: p5.Vector
let gravity: p5.Vector

let tWidth: number
let tHeight: number

let maxSize = 0

let dim
function setup() {
  dim = min(windowWidth, windowHeight) * 0.8
  maxSize = dim / 100
  createCanvas(dim, dim)
  velocity = createVector(0, 2.1)
  gravity = createVector(0, 0.2)

  textStyle(BOLD)

  tWidth = textWidth('モリサワ')

  loc = createVector(dim / 2, 0)

  fill(0, 4)
}

function draw() {
  if (!running) {
    return
  }

  loc.add(velocity)
  velocity.add(gravity)

  if (loc.y > dim) {
    velocity.y = velocity.y * -0.85
    loc.y = height
  }

  const p = map(dim - loc.y, 0, dim, 2, 10)
  textSize(maxSize * pow(1.5, p))
  tWidth = textWidth('モリサワ')
  if (loc.y / dim > 0.98) {
    return
  }
  text('モリサワ', loc.x - tWidth / 2, loc.y + textAscent())
}

function mousePressed(event: MouseEvent) {
  if (event.altKey) {
    running = !running
    return
  }

  running = true
  setup()
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