+++
title = "Video Textures"
description = "Video Textures visualization"
header_image = "images/vt/vt2.png"
math = true
showToc = true
+++

<!--more-->

This visualization is implementing Video Textures paper[^1]. Video texture is a type of media. It aims to generate potentionally infinite video stream from analyzed input frames. In comparasion to a GIF, video textures are striving to minimalize repetativity.


|  GIF approach | Video Texture approach  |
|---|---|
| {{< figure src="/images/vt/tutorial1.png" alt="Video Texture explanation" width="300px" class="content-img">}} | {{< figure src="/images/vt/tutorial2.png" alt="Video Texture explanation" width="300px" class="content-img">}} |

Another explanation is presented for example in following video.

{{< youtube id="Pt5rrjwW_1U" >}}


## The result

Live version of the Video texture player is available [here](https://vt-player.netlify.app), with list of all used examples including [clock](https://vt-player.netlify.app/clock.html) used in original paper [^1].


### DynTex database

Some examples used are from DynTex database [^2].
- [stairs1](https://vt-player.netlify.app/stairs1.html)
- [stairs2](https://vt-player.netlify.app/stairs2.html)
- [grass](https://vt-player.netlify.app/grass.html)

|Stairs1|                                              Original                                              |                                             Processed                                             |
|-----------|:--------------------------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------------------------:|
|             | {{< figure src="/images/vt/stairs0.gif" alt="stairs01" width="250px" class="content-img-center">}} | {{< figure src="/images/vt/stairs1.gif" alt="stairs1" width="250px" class="content-img-center">}} |
| Speed       |0%|73%|
| Probability |73%|73%|

[^2]: DynTex: a Comprehensive Database of Dynamic Textures [link](http://projects.cwi.nl/dyntex/)


### Cartoon

Example [cartoon](https://vt-player.netlify.app/cartoon.html) is from caroon called Goopy Geer, released in the year 1932. Animation style used in those kinds of cartoons is called rubber hose animation. The idea of using it as input for video texture analysis comes from an observation of their periodic motion.


## Matrices

To illustrate the process, similarity matrices and transition matrix were plotted.

### Similarity matrices

To visualize data from analysis, similarity matrices were plotted using *matplotlib*. Following picture (of [cartoon](https://vt-player.netlify.app/cartoon.html)) is showing distance, dynamics a future cost matrices. Future costs matrix is then mapped as probabilities of transition. Those values are then pruned by keeping just the local maximumas and trimming values lesser than given threshold.

{{< figure src="/images/vt/0_37.png" alt="Similarity matrices" width="450px" class="content-img-center">}}

### Transition matrix

Following picture shows [stairs1](https://vt-player.netlify.app/stairs1.html) transiton matrix. Frame indexes are plotted on $x$ and $y$ axes. In contrast to similarity matrices, transition matrix has only binary values, meaning only `True` and `False` values are plotted. True means that transition is possible.

{{< figure src="/images/vt/stairs1_transition.png" alt="Similarity matrices" width="450px" class="content-img-center">}}




## Implementation

Frame analysis was implemented in Python3. The code and usage is avalible at [Github](https://github.com/hoskra/vt). Interactive frame synthesis player was implemented using library *p5.js*.











[^1]: Schödl, Arno, et al. "Video textures." Proceedings of the 27th annual conference on Computer graphics and interactive techniques. 2000. [link](https://www.cc.gatech.edu/gvu/perception/projects/videotexture/SIGGRAPH2000/index.html)