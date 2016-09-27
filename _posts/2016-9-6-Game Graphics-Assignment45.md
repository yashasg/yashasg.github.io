---
layout: post
title: Game Graphics-Assignment 4.0
published: true
---


##Rendering using Indices!!.
<iframe width="640" height="315" src="https://www.cade.utah.edu/~gujjar/Assignment4/ass4screenshot.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~14 Hours.
[Download-Assignment 4.0](https://www.cade.utah.edu/~gujjar/Assignment3/game.zip)


_Purpose of the Assignment_:

The puirpose of the assignment was to update the way openGL and D3D render our meshes,it is not good for performance to send 6 vertices,instead,giving it 4 vertices and asking the shader to index is faster
_How I did the Assignment_:

_Like last I will go over my tasks based on the commits I made to GIT_.

_My First Commit_:

I started off getting rid of the warnings i had due to the rebuilding issue.This was fairly easy and felt content when there were no issues with rebuilding anymore.

_My Second Commit_:

I worked on adding a const index buffer to see if I could get this to work first.In retrospect I think this was a good idea but I feel like I spent too much time getting this to work.When I actually got it to work,I realised later that it was not the whole picture,and I was supposed to delete the temp folder to actually see the major changes.
 I learnt that rebuilding solution is a crucial process.

_My Third Commit_:

Here I started my journey in implementing Lua loader,and oh boy was it a gruelling experience,so much so that I still think it is really buggy.The problem was making my code modular,but also make it independent of the mesh class,which meant i had to deal with pointers and pointers to pointers and so on.Michael helped me out understanding why pointers to pointers to pointers actually makes no sense,but nevertheless this took me the most amount of time.

I closed shop after this and hoped I could complete D3D setup and the virtual function setup on Monday.

_My Fourth Commit_:

Right now I have a working version of the Lua loader,but my square doesnt show up on the screen.
I get a warning that says


D3D11 WARNING: ID3D11DeviceContext::Draw: Vertex Buffer at the input vertex slot 0 is not big enough for what the Draw*() call expects to traverse. This is OK, as reading off the end of the Buffer is defined to return 0. However the developer probably did not intend to make use of this behavior. 
[ EXECUTION WARNING #356: DEVICE_DRAW_VERTEX_BUFFER_TOO_SMALL]


I know this warning is a problem but I dont have the time or expertise to debug through the issue.


_My Fifth Commit_:

I made the changes to my openGL code as well and I still dont see my square,I am now positive that I dont quite understand how the data is being sent to the shader and read by it and I need to do more research so I can make the code work.

Submission Checklist:
I dont think I have a lot to show interms of the checklist,by game runs but no mesh is displayed.


The max vertices required to draw a is 4 and we need 6 indices to represent the vertices.


I think there is no maximum vertices my mesh can have(cosidering that a mesh need not only be a square or a triangle but any complex shape)


Same way I think my mesh should not have maximum triangles either as a square can have 2 but other shapes can have 3 or more.
The reason the mesh file needs to be human readable for this assignment is so that we understand the data that is being sent from the mesh to the renderer to the shader,I think understanding this will give a good perspective in troubleshooting in the future.

I built my Mesh witht he logic that vertex contains information about the position and color,and indices is encapsulated with the vertices in a single table.
Furthermore,as indices are used to draw the triangle i put them in a table of 3 indices each.so it is more readable.


I used the winding order of lefthanded,i chose this because direct3d is very perticular about left handed triangles,but openGL doesnt care,I did this to speed up my development process,In the future openGL will just read the array in decending order to draw the triangle
I set my color to read 4 values because it made sense for a color to have an alpha.


No I didnt push my mesh in a subdirectory,because I didnt have the time to work on that.I feel its a good design choice,and we should also have the shaders in their own directory


I have used ".lua" for my mesh asset extension,I would change it later,when I am done dealing with my current problems


Conclusions:Where there are problems in code and I feel like there is no prgress,I generally dont commit,because its not on my mind during that time,I know this is bad practice,what are your suggesstions so I keep commiting any changes I make so reverting and backtracking is easier.

Update: I finally got the code to work.I relised i made some dumb mistakes,

1) At one point i reverted my code to remove the index buffer because I had problems with shader,but then i forgot about it and started working on the Lua code, which cause the problem of the buffer not being rendered on screen.

2)Secondly,doing it in OpenGl would be so much more easier that D3D,I should have started witht hat so I could have something more to show for.

3)Pointer math is hard and pointer to pointer to pointer actually makes no sense and should be avoided.

4)Lua parsing was not as easy as I thought and modularity is not your friend when loading data from Lua file.

5)Architechturally I think having std:vectors to maintain buffer data is actually the best way to go about the Lua loading problem.I think I will do that now,to avoid future problems.

6)I think getting a high level overview of what we need to do in the assignment is important,so we can plan ahead on how much time each part takes.I think I just tried to take it one at a time,and spent a lot of time in the beginning parts of the assignment. 

