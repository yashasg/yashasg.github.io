---
layout: post
title: Game Graphics-Assignment 3.0
published: true
---


##Change in Graphics Architechture woohoo!!.
<iframe width="640" height="315" src="https://www.cade.utah.edu/~gujjar/Assignment3/ass3.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~12 Hours.
[Download-Assignment 2.0](https://www.cade.utah.edu/~gujjar/Assignment3/game.zip)

Gitlab Tag- Assignmentv3

_Purpose of the Assignment_:

The Purpose of the Assignment was for us to rewrite parts of the graphics architecture. so we could decouple the mesh drawing logic from the existing code.

_How I did the Assignment_:

_This time I will go over my tasks based on the commits I made to GIT_.

_My First Commit_:

I started off by making the suggested changes to the Luaexe project to avoid the rebuilding issue I had in assignment 2. Following the guidelines correctly there was no problem getting this to work correctly.

_My Second Commit_:

The next thing I did was make a header file for Meshes. I put very little thought into deciding if I choose a class or a struct because when I looked up online,it said that the only difference is that in a struct the members are public by default, and in a class, they are private by default.
The reason I picked a struct was because I wanted to try it out.

When I started writing the Mesh.h,it got messy pretty quickly. I tried to keep it clean but I still think it looks untidy.


<iframe width="640" height="315" src="https://www.cade.utah.edu/~gujjar/Assignment3/meshheader.PNG" frameborder="0" allowfullscreen></iframe>


I also made the platform dependent cpp files and added empty definitions of the functions.


_My Third Commit_:

In this commit, I started working with openGL,because D3d looked like it was a lot of work,and I was not ready for that kind of time commitment on my Birthday(Yes, I was working on the assignment on my birthday #being_an_adult).I actually started moving parts of the code from graphics.gl.cpp to Mesh.gl.cpp.I moved the createVertexBuffer function to my the mesh class, and then replaced all the local variables it created to member variables of my class.This was fairly easy,At this point, I didn't setup the virtual function and submitMesh method in my solution.In retrospect, I feel like I should have done,before considering openGL work to be complete.

I closed shop after this and hoped I could complete D3D setup and the virtual function setup on Monday.

 But on Monday I got a good understanding of how to setup the D3D side of code in class.I could avoid most of the problems my classmates faced because of this,the downside is I felt left out because I didn't feel like the active members of the discussion in class,due to my lack of knowledge in settingupD3d.

_My Fourth Commit_:

I started working on the D3d side of code on Tuesday,and I was starting to panic a little bit.I first made my context file as a singleton and added getters and setters to everything I could think of. Furthermore,I replace every line of code that used either swap chain,vertex buffer,device3d, and immediate context, this actually took me forever and in retrospect,it was a bad idea.The result of this mistake was my device was not rendering anything on the screen.I learnt from Samrat that we don't need to replace everything,just set the device3d and immediate context with a setter of the context.

I then moved on to setting up my virtual function, I started off making an update function as pure virtual in my Application.h file. which I defined in my Game as it inherits from the application class.

I also made a static function called submitTographics that takes the mesh as an argument. I call this function in my implementation of Update function in my game and send it my mesh that it needs to draw.
As the static function lives in cbApplication, I call it through the namespace and send it a mesh.

_My Fifth Commit_:

Now that D3d worked,I made the same changes to OpenGL and it worked well.Once of the problems was that I was not initializing the mesh in my constructor,so OpenGL was also not rendering anything.I figured it out soon enough.

Code in MyGame that submits to mesh

```eae6320::Application::cbApplication::sendToGraphics(m_Mesh);
```

Code in Graphics.gl.cpp to render the mesh

```// render of mesh.gl.cpp
        m_mesh->Render();
```


I feel like I committed too little in this assignment,which is not good practice, I think the reason is because I was battling some problems in the assignment and small changes I made to solve problems didn't feel significant enough to commit. Also what helped with debugging is checking the history of a CPP file to see how it worked before I made the change.