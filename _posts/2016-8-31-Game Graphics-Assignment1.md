---
layout: post
title: Game Graphics-Assignment 1.0
published: true
---


##Animated triangle woohoo!!.
<iframe width="640" height="315" src="https://www.cade.utah.edu/~gujjar/game.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~12 Hours.
[Download-Assignment 1.0](https://www.cade.utah.edu/~gujjar/game.zip)

_Purpose of the Class:

I think the purpose of ther class is for us to learn how to program for OpenGL and D3D.while keeping in mind that we are developing it for a game engine,so performance is top priority.

_Purpose of the Assignment_:

The Purpose of the Assignment was for us to learn the Engine Architecture provided by the professor
and setting up dependencies in the solution.Also to learn how the way the Engine hierarchy is
maintained.We also had to learn how a triangle is drawn and animated on the screen, using OpenGL and
Direct3D

_How I did the Assignment_:

_I broke down my Assignment into tasks_.

_My First task_:

was to read through the assignment page and its links to other pages, which took quite a lot of time,
especially because I was not just reading it but also trying implement the things that we were asked to
do in the example solutions. Understanding these example solutions was really helpful and it all came
together when I started to setup the solution for the main assignment.

_My Second Task_:

I started setting up my main solution taking the existing solution provided by JP.

_Sub Task 1_:

The Graphics project needed to be added to the existing framework. I probably created the
project 4-5 times and deleted it before I got it right. Visual studio doesn’t readily provide an
option for a class library by default. So the right way was to select a console application and
make changes when dele project creation wizard shows up. Even over there we need to check
the box for empty project and another library.Practice makes perfect and now I know how to
make an empty class library in my sleep. Once the Graphics project was created, I added
property sheets to it

_Sub Task 2_:

First thing I did was to setup property sheets. This needs to be done very early in the solution
setup so you can avoid problems that can arise without them. The property sheets were selfexplanatory
and its purpose was to have a rigid system for creating and moving files with no
manual interaction. Without them it would be challenging to make a deployable game.

_Sub Task 3_:

Once the property sheets were in and working, I got the files that needed to be in the project
and moved them to the physical location of the graphics project.I added the files to visual studio
and realied the files were written to be in folders. I setup similar hierarchy in windows and visual
studio to maintain consistency in the solution.

_My Third Task_:

Setting up project dependencies As the graphics project was a newcomer to the solution,
nobody knew it existed and were too shy to make friends with it.I went in as the cupid and started
adding dependencies to the graphics project. I just looked at the include files in Graphics.gl.cpp and
added the projects in the build dependency.
Now Visual studio knows that Graphics needs these libraries to be built before it can build, but it still
expects a part to the libraries directory and the lib file names, I also setup up different dependencies for
open GL and Direct3D.
Now my project was building, but I still couldn’t see the triangle on screen.

_My Fourth Task_:

BuildAllAssets is a project that uses the BuildSystem to copy the assets(shaders) to the data folder. I
went and added the shader files to the custom build step of the build all assets. And then I finally saw
the white triangle.

_My Fifth Task_:

Animating triangle: I must warn you I was very rusty with Math during the assignment(even now),so the instructions on the
shader files spoke about playing with sine and cosine so the triangles shows a good animation. I played
around with them and stumbled onto a good effect.

_code_:

Position- sin(elapsedtime)>1?Position+sin(elapsedtime):Position-sin(elapsedtime);

Using this instruction,moving vertices of the triangle made the triangle flip when the position +offset
value increased more than 1.This was cool in OpenGL as I could see the back of the triangle.I replicated
the same effect in D3D and when the triangle turned,it disappeared from the screen, made me stumble
onto the Handedness of the triangle concept we spoke in class.I am still experimenting witht his
effect,but I don’t understand the phenomenon very well.
This concludes my finding in Assignment 1.I must have missed a few details, please let me know if you
would like to know more(or less) next time.
