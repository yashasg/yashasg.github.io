---
layout: post
title: Game Graphics-Assignment 8.0
published: true
---


##Mesh and Shader Builder.
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment7/maya_export.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~6 Hours.
[Download-Assignment 7.0](http://cade.utah.edu/~gujjar/Assignment7/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to create and use executable builders for meshes and shaders that we made for our engine

_How I did the Assignment_:

This was a fairly easy assignment,with very little to write interms of code.The assignment was more towards understanding the use of builder executables and streamlining the process of building the assets needed for the game.

_My First Task_:

I started off with importing all the required project and files for the solution.I didn't think too much about how these new projects are being used within the solution,but I expected to learn about it during my development process.

_My Second Task_:

There was a small change in the AssetBuildSystem.lua file where I needed to specify a type of asset i wanted to build(meshes to be precise).In the future when we have a different asset,like materials,we have to add a new asset type.
 This was fairly easy to do no sweat.

_My Third Task_:
I ran into a little problem when I was trying to debug the AssetBuildSystem by providing Evironment variables and command arguments in the debugging window of visual studio.The problem was that I was giving the environment variables within
double quotes.Internally every path is added with double quotes anyway,so to escape my implicit double quote,Visual studio added a nasty "\" character,the result was that when the absolute path was concatenated with
AssetsToBuild.lua there were 3 "\" characters before AssetsToBuild.lua,and hence it was unable to find the file.Posting on the discussion helped me to see that I was being stupid with the environment variables.This was the only blocker for me in the assignments.

	
_My Fourth Task_:

In this task I went into the graphics library and made the prescribed changes to the vertex and the fragment shaders for d3d to load the binary file provided in the bin directory.This is one of the changes we made to the build process,.Instead of compiling and running the shader in runtime,we compile the d3d shader in build time
and saved the out code in a binary file. I chose not to make changes to the shader extension after it was built,because I would be a misinterpretation for the openGL shader file,as we are unable to compile and output the data of the openGl shader,it feels wrong to call it anything else than what it is.I am sure there is a way to just do it for the d3d shader,but 
it felt like too much work for a small achievement.


Some Questions Answered:
The AssetsToBuild.lua file is added to the BuildAllAssets project currently.The reason is mostly just ease of access,to the changes we want to make to the list.


The AssetBuildSystem required Meshbuilder.exe and ShaderBuilder.exe to move the assets to the data folder on the game,hence the AssetBuildSystem depends on them to function correctly.Dependencies in my understanding is what things are required for a process to complete successfully.If we look at dependencies as library dependencies,then there will be no projects that depend on the ShaderBuilder and MeshBuilder.
But I dont want these projects to feel lonely.So I gave them 1 friend :).


Advantages of AssetsToBuild.lua-Major advantage is we dont need to go an update mesh files and lua files in the custom build step everytime something in the game changes.


This way definitely looks cleaner.And also all the changes you want to make are in the file.


Changes in File Sizes of Binary and Authored files-there is a difference of around 1kb.Majorly because comments are ommited in the binary version of the file.Other than that we also have a few rules mentioned in the ShaderBuilder that specify what lines to omit based on the type of build that is taking place.Forexample the debug statements are removed for the release build 
In general debug mode is for making sure the code is doing what you expect it to do.In release you are all about optimisation and perfomance.Sorry for being abstract about this,I dont know specifically what is being removed in the release version of the shader.


I dont see a difference in the vertex.shader code for openGL in debug or release(atleast it is not less than 1KB,which I think windows just rounds it upto 1 KB) so it cool :).



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






