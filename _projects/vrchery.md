---
layout: page
title: VRchery
description: a fully immersive virtual reality archery sim built in Unity
img: assets/img/projects/vrchery/vrchery_prof.jpeg
importance: 3
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/vrchery/vrchery_gif.gif" title="sample screenshot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

I built this project alongside Vidit Agrawal and Kevin Tran as part of CMPSC 190I, a course on Virtual Reality. You can check out the project on GitHub [here](https://github.com/320trankt/VRchery) (although you'll need to open it in Unity to look at it in detail), or view the demo and presentation [here](https://docs.google.com/presentation/d/1JWvqR2X3e6UCbpImcjTUH9FcJ9UmlIy3Uhb7y37QVRY/edit?usp=drive_link). If you just want to see the demo you can view it [here](https://drive.google.com/file/d/11qNqonF8CI2HZZyUSIWC20jC2E5Zi8zQ/view?usp=drive_link).

The project contains several core components, all assets loaded in Unity and all scripting done with C#.

1. Bow and bowstring (ensuring that when the player pulls the bowstring back, the string render follows their pull)
2. Arrow physics (bowstring pullback should directly influence how far the arrow flies)
3. Target and environment (create a dynamic environment where arrows can land on trees, target, calculate points, etc.)

## Reflection

This was a really fun and interesting project! Coding scripts for physical interactions between simulated objects was very different from what I'm normally used to. Here are some of my reflections about the team and my own performance:

### Successes

We finished! The three of us had pretty little VR experience—Vidit and I had never touched Unity, Kevin had some, but not much in VR. 

Our overall process of scripting in C# was ok, we had a few online tutorials to look at in designing the physical mechanics of the bow and arrow (specifically calculating bowstring pullback and correlating it with launch velocity of the arrow), and it ultimately worked as we expected.

All Unity modeling was pretty fun; we selected all free, low-poly assets to save both money and make the rendering process a lot faster.

We also successfully worked with XR Interaction Toolkit, the Unity framework designed specifically for VR headsets and controllers, and used the XR Device Simulator well. 

Unfortunately we didn't have headsets to playtest with, so we settled with XR Device Simulator, which allows us to somewhat simulate the actual controllers. That's why you can see the controllers and their point rays in the screenshot. This was ultimately not a super big hiccup, just made filming the demo a little more complex. Ultimately ok.

Kevin, who owns a VIVE, did go back and test actual VR controllers after we completed the project. It worked! 

### Challenges

We finished, but there was definitely a lot to learn throughout! We spent a lot of time learning how to properly work with physics in the Unity UI; here are just a few hiccups we ran into:

1. grabbing the bow initially didn't lock it properly, so you would be holding it sideways
   1. solved with specific grab position lock with XR Interaction Kit
2. grabbing the arrow has the same issue, it would just be oriented wrong and fly the wrong way
   1. same solve as above, but we set the arrow orientation relative to the bow (which we didn't know we could do at first)
3. the bowstring is dynamic; we used a line render, but then we had to attach an additional grabble invisible box to simulate holding the bowstring; then pulling back would have to result in the bowstring bending appropriately, etc. 
   1. just spend a lot of time getting it to work and look normal, the bowstring was rendering the wrong direction for a solid hour before we found the problem (hint: we did the math wrong)
4. didn't know how to put the floor and the bow in the same layer, so the bow would fall through the ground into the void
   1. found the menu option eventually
5. arrow collision had similar issue to previous, with arrows fully disappearing into the void
   1. same as above

TODO: add a gif soon