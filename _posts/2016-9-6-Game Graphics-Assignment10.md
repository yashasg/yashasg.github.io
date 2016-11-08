---
layout: post
title: Game Graphics-Assignment 10.0
published: true
---


##Gameplay.
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/ass10.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~8 Hours.
[Download-Assignment 10.0](http://cade.utah.edu/~gujjar/Assignment10/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to create binary meshes to load into the game.As authored meshes take more space and time to read during runtime.

_How I did the Assignment_:

This was a fairly easy assignment because it was mostly about restructuring code,and add some code to read and write binary data.

_My First Task_:

I moved my lua helper functions that load the mesh during runtime to the meshbuilder,this brought in a bunch of dependencies so I had to go in and set the build dependencies and add additional include libraries for the Meshbuilder.With very minor chages to code,I was able to load the lua file data into memory during build time,next task was to write it into a file as binary data.


_My Second Task_:
I slowed down a bit here because I was dealing with pointer math a little bit and I also had a problem with writing out the vertex data information.JP helped me find my error in logic and then i went owards towards reading the data during runtime

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/meshbinss.PNG" frameborder="0" allowfullscreen></iframe>


_My Third Task_:
This part was fairly easy as most of the information was given in the instructions,one thing i was adviced to change and I changed was removing magic numbers.all my offsetting is done with sizeof operators,so there should be no inconsistency.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/reading%20binary.PNG" frameborder="0" allowfullscreen></iframe>

_My Fourth Task_:
This is the final part,I created a platform independent header for effects and platform dependent representations of it.One problem I had with loading member variables is that
because they were not in the scope of my helper functions I had to send the pointers address so the helper functions could manipulate that information.otherwise i would always be given a null pointer,so in short I did a pass by reference so the function could manipulate my pointer.Once this was done everything else was golden.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/binding.PNG" frameborder="0" allowfullscreen></iframe>
	

Some Questions Answered:
The way I have ordered my binary file is:

I have my vertex array size first,then my vertex array data,my index array size and index array data.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/meshbinss.PNG" frameborder="0" allowfullscreen></iframe>

Advantages of using Binary meshes over authored meshes:
Binary files are faster to load and also occupy less space on disk.Hence they are better to use by the game during runtime.

The advantage of human readable format is that firstly they are human readable so for debugging purposes we could actually see if there are any problems witht he mesh.

Hence its better to store the data in human readable format,so its easy to go through and find problems,but make a binary file for the runtime,so there is faster loading of data.

I think the binary meshes should be named the same for both platforms,because platforms have nothing to do with what kind of mesh is generated.Atleast not in our case,maybe in the industry,if we are building for consoles we might build a lower-poly mesh,but for open gl and d3d for PC it doesnt make any difference.


I downloaded a mesh that was 915 kb in my human readable file,but when I converted to binary the size came down to 200Kb.so we can say its around 4 times smaller.

Interms of load times the file took 0.5 seconds to load from the Lua file but only 0.0002 seconds when loading from a binary file,and this includes file read time.so its very fast.

Here is the platform independednt binding
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment10/binding.PNG" frameborder="0" allowfullscreen></iframe>

Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






