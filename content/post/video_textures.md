+++
title = "Video Textures"
description = "Video Textures project"
header_image = "images/vt2.png"
+++

<!--more-->
## About
This visualization is implementing Video Textures[^1]. 


## Implementation

Frame analysis was [implemented](https://github.com/hoskra/vt) in Python3.

Video Texture player was [implemented](https://github.com/hoskra/vt-player) in p5.js.
It is deployed to [Netlify](https://vt-player.netlify.app)


|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/stairs1_linear.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/stairs1_random.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/stairs1_random_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/stairs1_random_super_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |


|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/stairs2_linear.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/stairs2_random.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/stairs2_random_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/stairs2_random_super_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |


|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/ct1.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/ct2.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/ct3.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/ct4.gif" alt="Captured gif example" width="200px" class="content-img">}}  |



## Similarity matrices

{{< figure src="/images/0_37.png" alt="Similarity matrices" width="450px" class="content-img-center">}}


[^1]: Schödl, Arno, et al. "Video textures." Proceedings of the 27th annual conference on Computer graphics and interactive techniques. 2000. [link](https://www.cc.gatech.edu/gvu/perception/projects/videotexture/SIGGRAPH2000/index.htm
)
