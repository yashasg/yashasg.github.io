---
layout: post
title: Game Graphics-Assignment 8.0
published: true
---


##Gameplay.
<iframe width="640" height="480" src="http://cade.utah.edu/~gujjar/Assignment9/ass9.JPG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~6 Hours.
[Download-Assignment 9.0](http://cade.utah.edu/~gujjar/Assignment9/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to create a game using our Engine

_How I did the Assignment_:

This was a fairly easy assignment,I had to put some thought on gameplay.I started off thinking to make a first person shooter,but my ideas crumpled very soon because I didnt know how to get a forward vector based on my currect rotation
and position.So I decided to make a 2D space shooter,Alien Invaders, with 3D objects

_My First Task_:

I removed the control from the camera,and snapped the camera movement to the player.The player can move with a WASD command.


_My Second Task_:
Adding a bullet.

The player can shoot 1 bullet at a time.Another bullet can be shot only when the first bullet leaves the screen,just like in the game.


_My Third Task_:
I put some thought into my gameplay model.I currently have a namespace that does gameplay related things,but it still lives in the save mygame.cpp file.Ill change it later,once the code gets too complicated to maintain.
	

Some Questions Answered:

The plans for the future is to create enemies and then make them move and shoot to dodge attacks and attack the player.


The Game interacts with the Graphics engine using the set to graphics code that sends data to the graphics engine.


Like I mentioned before I have not added any new classes just a namespace of helper functions for Gameplay related code.i am still thinking on how Gameplay things can be added.In a different file or different project.


The only snippets of reusable code is the input code and SnapPlayerToCamera.



Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






