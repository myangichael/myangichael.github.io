---
layout: page
title: VRchery
description: a fully immersive virtual reality archery sim built in Unity
img: assets/img/12.jpg
importance: 1
---

I built this project alongside Vidit Agrawal and Kevin Tran as part of CMPSC 190I, a course on Virtual Reality. You can check out the project on GitHub [here]() (although you'll need to open it in Unity to look at it in detail), or view the demo and presentation [here](). 

The project contains several core components, all assets loaded in Unity and all scripting done with C#.

1. Bow and bowstring (ensuring that when the player pulls the bowstring back, the string render follows their pull)
2. Arrow physics (bowstring pullback should directly influence how far the arrow flies)
3. Target and environment (create a dynamic environment where arrows can land on trees, target, calculate points, etc.)