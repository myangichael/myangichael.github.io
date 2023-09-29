---
layout: page
title: VRchery
description: a fully immersive virtual reality archery sim built in Unity
img: assets/img/projects/vrchery/vrchery_prof.png
importance: 1
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/vrchery/vrchery_prof.png" title="sample screenshot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

I built this project alongside Vidit Agrawal and Kevin Tran as part of CMPSC 190I, a course on Virtual Reality. You can check out the project on GitHub [here](https://github.com/320trankt/VRchery) (although you'll need to open it in Unity to look at it in detail), or view the demo and presentation [here](https://docs.google.com/presentation/d/1nARqSpOlcpT2YiCXVa6TsuGfkKqxy836Dn2cmUqoko4/edit?usp=sharing). 

The project contains several core components, all assets loaded in Unity and all scripting done with C#.

1. Bow and bowstring (ensuring that when the player pulls the bowstring back, the string render follows their pull)
2. Arrow physics (bowstring pullback should directly influence how far the arrow flies)
3. Target and environment (create a dynamic environment where arrows can land on trees, target, calculate points, etc.)