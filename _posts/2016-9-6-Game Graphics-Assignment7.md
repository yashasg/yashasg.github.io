---
layout: post
title: Game Graphics-Assignment 7.0
published: true
---


##Maya Meshes.
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment7/maya_export.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~6 Hours.
[Download-Assignment 7.0](http://cade.utah.edu/~gujjar/Assignment7/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to import and render meshes from maya using a custom built plugin

_How I did the Assignment_:

This was a fairly easy assignment,with very little to write interms of code.The assignment was more towards understanding the tools that are used to export data from maya to the game.

_My First Task_:

I imported the MayaMeshExporter project and made the changes in the cofiguration to run only on x64.

_My Second Task_:

I downloaded the Maya2017 student edition and the sdk.Setting it up was fairly easy. And I got it to work very fast
 

_My Third Task_:
I went in and started making the required changes in the MayaMeshExporter project, i decided to give it the same extension name ".lua".It helped me make my workflow easy.

The MayaMeshExporter project depends on the Windows project in the engine to work.As per my understanding MayaMeshExporter project has no dependent projects,i.e none of the existing project require it to be functioning.

While writing the logic to write the mesh file,i saw other data that I didnt understand the usage,so I left it out,in the future I will have to go back and change it once I understand the use of the other data involved.

A problem I faced while writing to the file was that the floats were being written with full precesion which involved exponential values after decimal.I added the precision value to the fout field and also set the std::fixed,making the precesion of the data to only 2 values after the decimal.

I decided not to write in any comments into the file that was being generated,the reason being,the file has atleast a few hundred vertices and more indices.Expecting a human to go in and read it seems really optimistic.

A fun feature is the ability to debug the MayaMeshExporter plugin through visual studio,it helped me see if I was writing to the file correctly.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment7/debug_maya.PNG" frameborder="0" allowfullscreen></iframe>



	
_My Fourth Task_:

I went into Maya and loaded my plugin,I didnt come across any problems with that.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment7/may_plugin.PNG" frameborder="0" allowfullscreen></iframe>


Next I created my meshes and gave them each a color in the MeshColor tab in maya.
When I was creating the floor I also specified the width and height,and sometimes maya sets the translation vector to a wierd number,make sure it is correct.




Controls
Camera


Up arrow to move up

Down arrow to move Down

Left arrow to move Left

Right arrow to move Right


Space bar to zoom in


Control to zoom out

sphere
W to move up

A to move left

S to move down

D to move right.

The sphere,helix and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






