---
layout: post
title: Game Graphics-Assignment 11.0
published: true
---


##Effects for Materials.
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment11/animateshader1.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 11.0](http://cade.utah.edu/~gujjar/Assignment11/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to create binary effect files that will be used later to create materials.

_How I did the Assignment_:

This was a fairly easy assignment,but with a lot of things to do.As usual ill try to break down my tasks

_My First Task_:
I copied the new code to the AssetBuildSystem.lua, some of the static data and external functions added helped with adding a new Asset type called effect. I went in and added the code that returned the reference for the executable of effectbuilder,I then had to create a effect builder project and add a main function so the executable could be created.Even though the main did nothing,I was still able to see that the shader files mentioned in my effect were being moved to the $BuiltAssetDirectory.So it was all golden


_My Second Task_:
It was time to fill up the effectbuilder project,As the mesh builder and the shader builder I inherited from the cbbuilder class in the asset build library.And started to implement the lua functions that load from the table into memory.I had some problems with memcopying data from lua pointer,after copying,when i tried to free the program would crash. This is where _strdup helped,and I was able to free the allocated memory.The was I write my binary is,I put in the length of the first string(path to vertex shader) and then write the string.And the write a null character to signify the end of string character for my code during runtime.Same for the fragment shader path code.The reason I put the length of the string first is that during runtime i can access the path to fragment shader without any computation.
This is how my effect file looks when it is human readable

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment11/hreffect.PNG" frameborder="0" allowfullscreen></iframe>

And this is how it will look when I convert it to binary and store it as bineffect.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment11/bineffect.PNG" frameborder="0" allowfullscreen></iframe>

Another thing i chose to do during build time is prefix the path "data/" to my shader paths in binary.Data here is the relative path to the shader from the game.exe


Advantages of adding this during build time is that during run time there is no extra computation needed,it is as simple as reading the string and calling the function.

Disadvantage is that it takes up 10 extra bytes in the file,which might be expensive when  working with consoles or just reading file from disk takes time,and more data means more time.


This is how I am reading it in runtime


		```//get the starting position of the fragment shader path
		{
			fragmentPathstart = *reinterpret_cast<uint8_t*>(effectdata);
		}
		//get the path to vertex shader
		{
			o_pathVertShader = reinterpret_cast<char*>(effectdata + sizeof(fragmentPathstart));

		}

		//get the path to fragment shader
		{
			o_pathFragShader = reinterpret_cast<char*>(effectdata + sizeof(fragmentPathstart)+ fragmentPathstart*sizeof(char)+ sizeof(char));
		}
	}```


_My Third Task_:
Making a new effect,this was fairly easy.Coming up with a shader that did something different was the hardest path and I feel like I didnt have enough time to experiment with that.So my effect just move in local space slightly like a swing. I plan to use it as a shader for the background of space,make it seem like it is moving.

Here's one object with the swingy shader.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment11/animateshader1.PNG" frameborder="0" allowfullscreen></iframe>

Here's the changing color and local position of the mesh based on the shader.

<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment11/animateshader2.PNG" frameborder="0" allowfullscreen></iframe>

_My Fourth Task_:
Making my effect part of the gameobject.This was also fairly simple to do,once I knew what to do.So I moved the code around and got it to work


	

Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






