+++
title = "Kensuke Koike"
description = "Kensuke Koike inspired visualizations"
header_image = "images/penrose.png"
math = true
+++

<!--more-->

Visualizations are inspired by brilliant japanese artist [Kensuke Koike](https://kensukekoike.com). Two visualizations were made using web technoliges. This text is containing an explanation how was those visualizations made. An image used is from *Johann (Hans) Beckmann*, the name of the painting is *Im Inntal*.

| Circles                                                                                                                                                                         | Penrose                                                                                                                                                                                            |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| First visualization is made with [p5.js](https://p5js.org/). Online editor with source code is available at [p5 editor](https://editor.p5js.org/hoskra/sketches/EIpGW_LYt). | Another visualization was made with [three.js](https://threejs.org/). Live version reacting to mouse movement is available [here](https://metaviz-code.netlify.app/src/kensukekoike/penrose.html), online code editor [here](https://codesandbox.io/s/sharp-kare-9tzyfp). |
| {{< figure src="/images/kensok/kk.png" alt="Circles" width="300px" class="content-img-center">}}                                                                                | {{< figure src="/images/kensok/6.gif" alt="Penrose triangle" width="300px" class="content-img-center">}}                                                                                           |                                                                                     |


## Penrose triangle

There is not only one way to determine the coordinates of the Penrose triangle points. In this section will be explained the method used in the visualization.


{{< figure src="/images/kensok/kk0.png" alt="Penrose triangle" width="200px" class="content-img-center">}}

The idea here is to divide the penrose triangle into three shapes (yellow, cyan, pink) and get their coordinates.

{{< figure src="/images/kensok/kk1_.png" alt="Penrose triangle" width="250px" class="content-img-center">}}

First, we define the height of the triangle. The sum of all angles in any thiangle is 180 degrees. This triangle is equilateral and therefore all the angles has $180/3 = 60$ degrees. Using goniometric functions we express the height using a side of the triangle:

$$ tan(60\degree ) = \frac{h}{s/2} $$
$$ h = \frac{s}{2} * tan(60\degree ) $$
$$ h = s* \frac{\sqrt{3}}{2}.$$


For the inner triangle of the Penrose triangle, points $A$, $B$, $C$ and vectors $u$, $v$, $w$ were defined[^1] as:
<!-- | Points  | Vectors |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| $$ A = \[ -\frac{s}{2}, h*\frac{1}{3} \]$$                 | $$ u = \[ B - A \] $$                                                                                       |
| $$ B = \[ \frac{s}{2}, h*\frac{1}{3} \]$$                  | $$ v = \[ C - B\] $$                                                                                        |
| $$ C = \[ 0, -h*\frac{2}{3} \]$$                           | $$ w = \[ A - C \] $$                                                                                       |                                                                             |
|  -->

{{< figure src="/images/kensok/kk2_.png" alt="Penrose triangle" width="400px" class="content-img-center">}}


$$ (A,B,C) = (\[ -\frac{s}{2}, h*\frac{1}{3} \], \[ \frac{s}{2}, h*\frac{1}{3} \], \[ 0, -h*\frac{2}{3} \])$$

$$ (u,v,w) = (\[ B - A \], \[ C - B\],\[ A - C \] ).$$


Then, the coordinates for grayed shape ($x_1$, $x_2$, $x_3$, $x_4$, $x_5$, $x_6$) were expressed as a combination of vectors $u$, $v$, $w$.

{{< figure src="/images/kensok/kk3_.png" alt="Penrose triangle" width="400px" class="content-img-center">}}


For every $x_i$ coordinate, the origin was shifted to the point $A$.


```
x1 = A
x2 = A +   0  * u +   0  * v +  (-2) * w
x3 = A +   2  * u + (-2) * v +    0  * w
x4 = A +   3  * u + (-1) * v +    0  * w
x5 = A +   0  * u +   1  * v +  (-3) * w
x6 = A + (-1) * u +   0  * v +    0  * w
```
This is just an example of linear combination, that is generating this shape. There are more ways this points could be obtained.


{{< figure src="/images/kensok/kk4.png" alt="Penrose triangle" width="400px" class="content-img-center">}}


The next step is to generate the remaining two shapes. Those can be done using the same linear combination as before, but using the vectors $u$, $v$, $w$ in different order and thus performing a rotation. An example of another shape:


```
y1 = C
y2 = C +   0  * w +   0  * u +  (-2) * v
y3 = C +   2  * w + (-2) * u +    0  * v
y4 = C +   3  * w + (-1) * u +    0  * v
y5 = C +   0  * w +   1  * u +  (-3) * v
y6 = C + (-1) * w +   0  * u +    0  * v
```

The coordinates for the third shape can be generated analogouslly. Thanks to this process, the coordinates of those three shapes forming Penrose triangle can be generated and parametrized by the side of the inner triangle.


### Three.js

This code explains the *Three.js* implementation of the visualization. Coordinates are generated as was described above. Following code snippets are showing just specific part of the code.


```js
// function creates one shape from given coordinates and adds a texture to it
function penrosePart(coordinates, image_path, scene) {
  // load texture
  let texture = new THREE.TextureLoader().load( image_path );

  // enable mirror wrapping
  texture.wrapS = THREE.MirroredRepeatWrapping;
  texture.wrapT = THREE.MirroredRepeatWrapping;

  // create texture material
  let textureMaterial = new THREE.MeshBasicMaterial( { map: texture } );

  // create geometry from coordinates
  let geomShape = new THREE.ShapeBufferGeometry( new THREE.Shape( coordinates ) );

  // create mesh and add to scene
  let mesh = new THREE.Mesh(geometry, material);
  scene.add(mesh);
}
```

The visualization is reacting to mouse movement (and touch event). Mouse (or touch) coordinates are used to offset the shape texture.

```js
// edit texture offset on mouse move
function onDocumentMouseMove(event) {
  event.preventDefault();
  mouse.x = (event.clientX / window.innerWidth ) * 2;
  mouse.y = (event.clientY / window.innerHeight) * 2;
  shapeA.material.map.offset.x = positionX + Math.cos(mouse.x) * 0.3;
	shapeB.material.map.offset.y = positionY + Math.cos(mouse.y) * 0.3;
	shapeC.material.map.offset.x = positionX + Math.cos(mouse.y) * 0.3;
}
```


[^1]: This definition is using p5.js coordinate system, which has positive values in the right down corner.