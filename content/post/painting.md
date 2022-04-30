+++
title = "Painting"
description = "Mouse reactive visualization"
header_image = "images/painting.png"
math = true
showToc = true
+++

<!--more-->

Visualization is made with [p5.js](https://p5js.org/). Live version reacting to mouse movement is available [here](https://metaviz-code.netlify.app/src/painting.html).



{{< figure src="/images/painting/7.gif" alt="Painting" width="450px" class="content-img-center">}}

Live editor is available [here](https://editor.p5js.org/hoskra/sketches/lHnYDkjbv).

### Mona Lisa Effect

Mona Lisa Effect, is the feeling that no matter where you move in relation to a figure in an artwork, the eyes in the image follow you. In case of this visualization, it is not only a feeling.

## Code

This visualization is made with [p5.js](https://p5js.org/).
Those are the two artworks, that inspired this visualization:
- [hexagons](https://twitter.com/SnowEsamosc/status/1485932698036482051),
- [following eyes](https://editor.p5js.org/khamiltonuk/sketches/9LTXJPAoE).


<!-- `setup()`

`draw()` -->


### The Hexagon

{{< figure src="/images/painting/p0.png" alt="Painting" width="150px" class="content-img-center">}}

For this *sketch*, hexagon is drawn using `drawHexagon()`. Live example is available [here](https://editor.p5js.org/hoskra/sketches/bP9j3fgsI).


```js
function drawHexagon(x, y, radius) {
  beginShape()
  for(i = 0; i < 6; i++) {
    vertex(x + radius*cos(PI/3*i),y + radius*sin(PI/3*i))
  }
  endShape(CLOSE)
}
```

The code[^2] can be explained using the unit circle. In it, the position of the point on the circle is determined by the angle like this: $x=[cos(\alpha), sin(\alpha)].$

[^2]: *P5.js* does not require to declare variable names.

{{< figure src="/images/painting/t0.png" alt="Painting" width="300px" class="content-img-center">}}

<!-- |                                             Unit circle                                             |                                               Hexagon                                               |
|:---------------------------------------------------------------------------------------------------:|:---------------------------------------------------------------------------------------------------:|
| {{< figure src="/images/painting/t0.png" alt="Painting" width="300px" class="content-img-center">}} | {{< figure src="/images/painting/t1.png" alt="Painting" width="300px" class="content-img-center">}} |
 -->



Hexagon is regular polygon with 6 sides. The angle of each side is $\frac{360°}{6}=60$ degrees, or $\frac{2\pi}{6}=\frac{\pi}{3}$ radians.


{{< figure src="/images/painting/t1.png" alt="Painting" width="200px" class="content-img-center">}}

Therefore, the points of hexagon can be expressed as:

$$x_i = [cos(i*\frac{\pi}{3}), sin(i*\frac{\pi}{3})].$$


### The Eye
Live version of the eye is availible [here](https://editor.p5js.org/hoskra/sketches/UrsbDt3-N).
{{< figure src="/images/painting/eye.gif" alt="Painting" width="200px" class="content-img-center">}}

#### The Eyelids

The eyelid shape is drawn using two *p5.js* `arc()`[^1].

  [^1]: https://p5js.org/reference/#/p5/arc


```js
function drawEyelids(x,y) {
   off=PI/15
   arc(x, y-7, 70, 50, 0+off, PI-off)
   arc(x, y+7, 70, 50, PI+off, TAU-off)
}
```
#### The Iris

The iris is drawn with a circle. Instead of determining its position, the canvas is shifted to the center of the eye. Then, the angle between the center of the eye and the mouse position is calculated using $atan2(y,x)$.

{{< figure src="/images/painting/t3.png" alt="Painting" width="200px" class="content-img-center">}}

Then, the whole canvas is rotated by that angle. The distance between mouse and the center of the eye is used to determine how far the iris should be drawn. Functions `push()` and `pop()` are called to save and restore the state of the canvas. Without using those functions, the translations and rotations would stack up later.

```js
function drawEyes(x, y) {
  push()

  // shift to given coordinates
  translate(x, y)

  // get distance position from point [x,y]
  let distance = dist(x, y, mouseX, mouseY)

  // map distance with bounds being [0,500] to lenght [0,10]
  let mappedDistance = map(distance, 0, 500, 0, 10)

  // get vector to the mouse
  let v2 = createVector(mouseX - x, mouseY - y)

  // get angle between vector and center of the eye and rotate canvas
  let angle = atan2(v2.y, v2.x) + PI/5
  rotate(angle)

  // draw iris on the coordinates of mapped distance
  circle(mappedDistance, mappedDistance, 30)
  pop()
}
```

This [example](https://editor.p5js.org/hoskra/sketches/UcEISwlTw) can maybe make it easier to illustrate.

{{< figure src="/images/painting/eye1.gif" alt="Painting" width="200px" class="content-img-center">}}

### Complete visualization

Visualization is using functions `drawHexagon()`, `drawEyes()` and `drawEyelids()` explained above. Shapes are drawn to form a hexagon grid.


```js
function draw() {
 let s = sqrt(3)

 for(h = 0; h < W+100; h += 50) {
   for(w = -h*s; w < W+100; w += 100*s) {
     stroke(255)
     strokeWeight(15)
     drawHexagon(w,h,100/s)

     noStroke()
     fill(255)
     drawEyelids(w,h)

     fill(0)
     drawEyes(w,h);
   }
 }
}
```