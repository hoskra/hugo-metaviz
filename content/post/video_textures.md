+++
title = "Video Textures"
description = "Video Textures visualization"
header_image = "images/vt/vt2.png"
+++

<!--more-->

This visualization is implementing Video Textures paper[^1]. Video texture is a type of media. It aims to generate potentionally infinite video stream from analyzed input frames. In comparasion to a GIF, video textures are striving to minimalize repetativity.


|  GIF approach | Video Texture approach  |
|---|---|
| {{< figure src="/images/vt/tutorial1.png" alt="Video Texture explanation" width="300px" class="content-img">}} | {{< figure src="/images/vt/tutorial2.png" alt="Video Texture explanation" width="300px" class="content-img">}} |

Another explanation is presented for example in following video.

{{< youtube id="Pt5rrjwW_1U" >}}



## Implementation

Frame analysis was implemented in Python3. The code and usage is avalible at [Github](https://github.com/hoskra/vt). Interactive frame synthesis player was implemented using library *p5.js*. Live version is avalable [here](https://vt-player.netlify.app).


## Similarity matrices

To visualize data from analysis, similarity matrices were plotted using *matplotlib*. Following picture is showing distance, dynamics a future cost matrices. Future costs matrix is then mapped as probabilities of transition. Those values are then pruned by keeping just the local maximumas and trimming values lesser than given threshold.

{{< figure src="/images/vt/0_37.png" alt="Similarity matrices" width="450px" class="content-img-center">}}


### The results

Following recordings are the result of implemented algorithm played by implemented player.
Videos used are from DynTex database [^2].

[^2]: DynTex: a Comprehensive Database of Dynamic Textures [link](http://projects.cwi.nl/dyntex/)

|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/vt/stairs1_linear.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/vt/stairs1_random.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/vt/stairs1_random_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/vt/stairs1_random_super_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |


|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/vt/stairs2_linear.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/vt/stairs2_random.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/vt/stairs2_random_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/vt/stairs2_random_super_cross.gif" alt="Captured gif example" width="200px" class="content-img">}}  |

Following example is from caroon called Goopy Geer, released in the year 1932. Animation style used in those kinds of cartoons is called rubber hose animation. The idea of using it as input for video texture analysis comes from an observation of their periodic motion.

|        | No Crossfading | Crossfading | Super Crossfading |
|--------|----------------|-------------|-------------------|
| Linear |       {{< figure src="/images/vt/ct1.gif" alt="Captured gif example" width="200px" class="content-img">}}          |      -      |         -         |
| Random |       {{< figure src="/images/vt/ct2.gif" alt="Captured gif example" width="200px" class="content-img">}}         |   {{< figure src="/images/vt/ct3.gif" alt="Captured gif example" width="200px" class="content-img">}}  |   {{< figure src="/images/vt/ct4.gif" alt="Captured gif example" width="200px" class="content-img">}}  |





[^1]: Schödl, Arno, et al. "Video textures." Proceedings of the 27th annual conference on Computer graphics and interactive techniques. 2000. [link](https://www.cc.gatech.edu/gvu/perception/projects/videotexture/SIGGRAPH2000/index.html)