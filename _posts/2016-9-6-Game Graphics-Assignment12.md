---
layout: post
title: Game Graphics-Assignment 12.0
published: true
---

#Materials with effects.
<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment12/materialgame.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 11.0](http://cade.utah.edu/~gujjar/Assignment12/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to create binary create materials that have different parameters and effects.

_How I did the Assignment_:

This was a fairly easy assignment, I started a bit late but I was able to complete it within 7 hours.

_My First Task_:
I was curious to see if I could accomplish having an plaform independent cpp file for graphics,so I spent around 2 hour setting that up,i tried different ways,but finally settled for a platform independent singleton class called GraphicsHelper with platform dependent implementations.It fit well with my existing code,and I tried to avoid using member variables completely,so my only member variable is my singleton instance,everything else is a static variable only exposed to the platform dependent data


_My Second Task_:
I started off with making changes to the shader files. The instructionns were kind of unclear as to where the layout needs to be defined,I realised I could do them anywhere,so i did them at both places,the vertex and the fragment shader.I dont know if its the right way,but it works.


_My Third Task_:
I made a new project for effect builder and added the code to create a binary effect file during debugging,this makes it easier to narrow down on any problems that could arise with the exe,once this was sorted I added the code in the assetbuildsystem.lua to add the refernced effect files and a new asset type called materials.

This is how my human readable material file looks like

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment12/redmat.PNG" frameborder="0" allowfullscreen></iframe>

The material table represent all possible things it can have,for now I only have color,but I can add more stuff based on specifications. This is setup in such a way that even if the material table was empty I am writing my binary file with default data,that way during runtime I can just load it and run it.

Here's how my material file looks when in binary.

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment12/binmat.PNG" frameborder="0" allowfullscreen></iframe>

As you can see I differentiated each float value(4 bytes).This is the color data that I have stored,and if you look closely,it is the color red,with full opacity.

the second path of the binary file is the path to the effect that it is using.

There is a reason i formatted my binary file in such a way that my constant data comes first and then my variable data.This way I dont need to store a byte data of where my path string ends and my material data starts.I saved a byte of data and a little bit of computation in runtime.Cool,right!

_My Fourth Task_:
Here's what my Game looks like right now.

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment12/materialgame.PNG" frameborder="0" allowfullscreen></iframe>

The other plane is the opponents plane and we can see its different because it is changing color.I want to make many of these and they change different colors so they all look different.

Since the first time I decided on the game I have added a bullet and now an oppenent model,interms of gameplay I reset the bullet once it leaves the screen and now my opponent also has his own bullet to shoot me with. I play to add some basic AI on opponents that will soot at the player. So far I didnt change any plance since assignment 9.

	

Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






