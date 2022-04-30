+++
title = "Crown Shyness"
description = "Crown Shyness visualization using Voronoi tessellation"
header_image = "images/cc3.png"
+++

<!--more-->

Crown shyness[^1] is a phenomenon observed in some tree species, in which the crowns of fully stocked trees do not touch each other, forming a canopy with channel-like gaps. Following photograph is showing the phenomenon.


[^1]: Possible explanations why Crown shyness occur can be found for example in paper: *Crown shyness in various tree species*; Rishabh Hattimare; 2018; [link](https://www.ijsdr.org/papers/IJSDR1812056.pdf)

{{< figure src="/images/crown_placeholder.jpg" alt="crown" width="400px" class="content-img-center">}}



## Implementation

This effect was simulated with Voronoi tessellation. Visualization was implemented in [p5.js](https://p5js.org/) and [three.js](https://threejs.org/).

Visualization is available [here](https://metaviz-code.netlify.app/src/crown-shyness/7/index.html). This visualization has more color themes. One is picked at random at the start of the visualization.

{{< figure src="/images/cs/5.gif" alt="crown shyness" width="450px" class="content-img-center">}}

### Description

The idea about this visualization is to use Voronoi tesellation to generate crowns of the trees. Following image is showing the terminology behind the tesellation.

{{< figure src="/images/cs/voronoi.png" alt="voronoi" width="450px" class="content-img-center">}}

First step was to obtain generator points. That was done using similar like in this [circle packing](https://www.youtube.com/watch?v=XATr_jdh-44) example.

{{< figure src="/images/cs/points.png" alt="points" width="350px" class="content-img-center">}}

Then, library [d3-delaunay](https://github.com/d3/d3-delaunay) was used to get Voronoi tesellation. The rest was possible thanks to *WEBGL* renderer, allowing to use perspective. Previous versions are more complex, but computationally expensive.
### Previous versions

This visualization had more iterations. versions 1 and two were implemented using *p5.js*.
|Version 1 | Version 2 |
|:---:|:---:|
| {{< figure src="/images/cs/v1.png" alt="crown shyness" width="300px" class="content-img">}}   |  {{< figure src="/images/cs/2.gif" alt="crown shyness" width="300px" class="content-img">}} |
| [online](https://metaviz-code.netlify.app/src/crown-shyness/1.html)   | [online](https://metaviz-code.netlify.app/src/crown-shyness/2.html)  |
| [source code](https://github.com/hoskra/metaviz/blob/main/src/crown-shyness/1.html)| [source code](https://github.com/hoskra/metaviz/blob/main/src/crown-shyness/2.html)|

Versions 3 and 4 implemented in *Three.js*.

|Version 1 | Version 2 |
|:---:|:---:|
|{{< figure src="/images/cs/3.gif" alt="crown shyness" width="300px" class="content-img">}}  | {{< figure src="/images/cs/4.gif" alt="crown shyness" width="300px" class="content-img">}} |
| [online](https://metaviz-code.netlify.app/src/crown-shyness/5.html)| [online](https://metaviz-code.netlify.app/src/crown-shyness/6.html)  |
| [source code](https://github.com/hoskra/metaviz/blob/main/src/crown-shyness/5.html)| [source code](https://github.com/hoskra/metaviz/blob/main/src/crown-shyness/6/index.html)|



<!-- - [version1](https://metaviz-code.netlify.app/src/crown-shyness/1.html)
- [version2](https://metaviz-code.netlify.app/src/crown-shyness/2.html)
- [version3](https://metaviz-code.netlify.app/src/crown-shyness/5.html)
- [version4](https://metaviz-code.netlify.app/src/crown-shyness/6.html)
- [version5](https://metaviz-code.netlify.app/src/crown-shyness/7/index.html)
 -->


