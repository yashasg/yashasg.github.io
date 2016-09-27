---
layout: post
title: Game Graphics-Assignment 5.0
published: true
---


##Moving Square!!.
<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment5/ass5screenshots.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 4.0](http://cade.utah.edu/~gujjar/Assignment5/game.zip)


_Purpose of the Assignment_:

The purpose of this assignment was to create constant buffers for frame data and mesh position data.We also added controls to the square to move it around the scene.
_How I did the Assignment_:

_Like last I will go over my tasks based on the commits I made to GIT_.

_My First Commit_:

I started with the reading that was given for the assignment.Unlike last time this time I went through the whole thing trying to understand everything before I got started.In retrospect,this wasnt the best idea.It took me a lot of time to understand what is going on in the reading,because looking at the whole picture and minor details at the same time is kind of hard.

I spent a couple of hours on this,but I got started with making my new structs DrawCall and Frame.Due to overcomplicating stuff in my mind,i tried maintaining constant buffers in these structs,after an hour i realised I was doing it completely wrong,and had to almost start over.

_My Second Commit_:

Once my structs were ready and logical,I started moving code to create a frame buffer to my ConstBuffer class. After many iterations on my ConstBuffer class it looks like this right now

<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment5/ConstBuffer.PNG" frameborder="0" allowfullscreen></iframe>


In this class we have 3 types of constant buffers,the way I allow my users to specify them is through an enum called BUFFERTYPE, it can specify 3 kinds of buffer types which are Frame buffer, Draw call buffer and material buffer.

This is a nice way of having a symbolic way of representing a const buffer.

for example the user specifies frame constant buffer by BUFFERTYPE::FRAMEBUFFER.

this tells me the type of const buffer the user is trying to initialize and with the logic i bind it to register 0,which maintains the time elapsed since last frame.

Cleaning up constant buffers.

I made a cleanup function in my constant buffer implementation that releases the memory and nulls the pointer.

To ensure I clean up before the API objects themselves is to call the cleaning before cleaning up the API objects.


_My Third Commit_:

Once my frame buffer was satisfactory I moved on to making the draw call buffer on the mesh,I was still dealing with only 1 mesh so I was hoping it would be simple.It worked at first,but it was only afterwards in this assignment I realised that I had to change a bunch of things. even within the same buffer.


The way I send the draw call to my graphics system is through 2 interfaces, my game code doesnt directly speaks to graphics,it speaks through the application to graphics,
for that interfact to work the game sends a 


```sendToGraphics(Mesh* i_Mesh, float squarePos_x,float  squarePos_y);```

which intern calls the below function to graphics

```eae6320::Graphics::SubmitMesh(Mesh* i_mesh,float i_x, float i_y);```

Once my graphics system receives it,I add the mesh to the list and the draw them in the render frame like below 

```	//update and bind drawcallbuffer
	{	size_t numOfMeshes = m_MeshCenters.size();
	for (size_t i = 0;i < numOfMeshes;i++)
	{
		sDrawCall currentMesh;
		currentMesh.g_objectPosition_screen[0] = m_MeshCenters[i].x;
		currentMesh.g_objectPosition_screen[1] = m_MeshCenters[i].y;
		s_DrawCallBuffer ->Update(&currentMesh,sizeof(sDrawCall));
		m_currentMeshes[i]->Render();
	}
	m_currentMeshes.clear();
	m_MeshCenters.clear();
	}
	```
	
	
_My Fourth Commit_:

I started off trying to offset my vertex center,I was not aware that the logic was in the shader.Kun Cheng an amazing programmer helped me find that.After that changing the offset is just about changing the values in the lua file.which was fairly easy.

The part that got me was,when we bind the constant buffer to registers there is an integer to specify which register to bind to,I never changed this,so I had this problem of only 1 mesh being drawn at a time. I also had problems with the data that I maintained after loading the lua file,the next mesh i read appeneded to the existing mesh vertices and indices.This problem was fairly easy to solve.
I spent a couple of hours trying to figure out why only 1 mesh was being drawn at a time.

But a good thing is while I was trying to solve this problem I solved the problem of my d3d vertex buffer being too small.The issue was that I was doing 2 draws in my render,DrawIndexed and draw.Once I got rid of it,the errors took care of themselves.

Everytime I fixed something for one platform, I had to go back and fix it for the other,and going back and forth I sometimes found bugs in 1 that helped me with other platform, so thats a good thing.


_My Fifth Commit_:

The previous part is where I mostly was stuck during my time on the assignment.The last part was having controls.
Right now the way my square moves is


Up arrow to move up

Down arrow to move Down

Left arrow to move Left

Right arrow to move Right

The square also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.



