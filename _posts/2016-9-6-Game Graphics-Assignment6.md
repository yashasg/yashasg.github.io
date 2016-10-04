---
layout: post
title: Game Graphics-Assignment 6.0
published: true
---


##Moving Square!!.
<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment6/rotating_cube.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 5.0](http://cade.utah.edu/~gujjar/Assignment6/game.zip)


_Purpose of the Assignment_:

Purpose of the assignment was to render our objects in 3d,and also have depth buffering.

_How I did the Assignment_:

This time I gave a brief reading of the requirements and then got changing code very soon.This was really a good idea.I felt like i understood more as I kept writing code. I also made a lot of commits in this assignment,every time i felt like this are working i did a commit and moved on to changing it.
This helped me revert back to a working version very fast.

_My First Task_:

I replaced the current vertices and Math files with the new ones,just so I can avoid any problems in the future.


I also enabled culling in openGL.This was fairly easy and I also added an assert to check if there were any errors when enabling it.


Encapsulating in the same task I also added a 3rd position on the lua file.The new positions didnt render the cube in 3d but I was able to see a square covering the whole screen.
This was because I didnt have a camera to transform location and position.Once I added the camera and keep it away from the cube,it wont cover the whole screen.

_My Second Task_:

When I made changes to the lua file,I had some hardcoded values in my lua file load that were causing unwanted behavior.I got rid of them and checked it in.
I also updated the code in the fragment shaders with the one in vertex shaders to maintain consistency and avoid linker errors.
After this I was able to render the square that had 3 coordinates.

I also decided to encapsulate my mesh and its transform in a GameObject. This helps with moving data among functions

Adding a Camera:
From my understanding of Unity, Camera is also a gameobject but has other properties. So I have a Camera struct that has a component called gameobject that is responsible for the position and orientation of the camera.
I also added other functionalities to my camera which calculated  a WorldToCameraTransformationMatrix and a CameraToScreenTransformationMatrix.
Here's my interface for the camera.


<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment6/rotating_cube.PNG" frameborder="0" allowfullscreen></iframe>
 

_My Third Task_:

Converting my square into a cube,this was kind of confusing for me because in OpenGl it was as simpleas changing a number from 2 to 3 which mainted the count of the vertices.But in d3d i didnt find that variable,my assumption was d3d does it
default,but I was wrong,we needed to change a define for D3d.Once that was done I was able to see the side faces of the cube.
	
_My Fourth Task_:

Rotating the cube,
This was very easy to do in D3D.I just had to made a new quaternion every frame and send it to my d3d graphics,but on openGL the data gets currupted when moving from one function to another.I am still unable to figure out
the problem that is causing this.So I just left my cube non rotating in openGL and added all functionalities,

Troubleshooting ideas I implemented:

Generally when class data is being passed thru functions,there are 2 things that are commonly used.
Assignment operator and copy constructor, I defined both of them for the quaternion

Update:

This problem was solved.

Michael helped me figure out the problem,

The problem was 
#define EAE6320_GRAPHICS_ISDEVICEDEBUGINFOENABLED

This code is defined in the Configuration.h file,which graphics.h includes.

But the cMyGame.cpp does not include, so my cMyGame.cpp considers the size of my gameobject to be 8 bytes more(2 GLuints) than what my graphics considers it during debug time.

So when I create my gameobject in cMyGame.cpp it is 48 bytes(because the #define is not something my game will consider.)

But when the data is passed into my graphics it is just 40 bytes.its is still the same struct,but the graphics project visualises the struct with the #define included. which means its going to ignore the 2 GLuints in the struct. and bring down the size to 40 bytes.

The way we figured this out was way complicated, I am glad Michael has the expertise to understand assembly. What we noticed that in assembly code,the way it was offsetting to get the rotation vector was through 20h.which means it was jumping 2 floats ahead and trying to read they bytes from there.

We noticed this anomaly because the myGame.cpp was only offsetting with an 18h.

So we went and commented out the #define in te configuration.h and voila. everything works.

I tried to articulate as much as I can,but if anyone wants to add anyuthing please feel free.


This problem has taken more than 8 hours of my time trying to figure out.
 


_My Fifth Task_:

Enabling depth buffering,

Adding the depth buffering was fairly easy,the code was given and we just had to know to add it in the right places.Once all the code was added,depth buffering was enabled.

I also added the floor.lua file at this point so I can keep the cube on the floor. this is just a plane,so I layed it on the y axis plane.And I had the cube.

This is how the cube should be when culling is enabled.

<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment6/cullingcube.PNG" frameborder="0" allowfullscreen></iframe>

Controls
Camera


Up arrow to move up

Down arrow to move Down

Left arrow to move Left

Right arrow to move Right


Space bar to zoom in


Control to zoom out

Cube
W to move up

A to move left

S to move down

D to move right.

The cube and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.

Questions Answered:

Vertices required for the cube when doing index drawing is 8 vertices.As compared to vertex drawing where would have to repeat atleast 1 vertex for every triangle. we would need 2 triangles for each face so we would need to draw 12 triangles.
As I mentioned we need to send atleast 1 vertex repeatedly drawing 12 triangles would require 36 vertices, which is 98 floats.breaking it down more it is 392 bytes of data.

By using indexed drawing we have 8 vertices which 24 floats and 96 bytes and we use 72 bytes to store indices.on the whole the number comes to 168 bytes,which is less than half of what we would have if we did vertex drawing.

We save 224 bytes on the whole,by using index drawing.

Interface for my Camera

<iframe width="640" height="315" src="http://cade.utah.edu/~gujjar/Assignment6/cullingcube.PNG" frameborder="0" allowfullscreen></iframe>

For the Gameplay programmer Camera is also a gameobject that he needs to submit to the graphics.So I overloaded the submitToGraphics function to also b e able to take int he camera.The Graphics interface has 2 functions submitMesh and SubmitCamera.
There is no abstraction here because the graphics needs to be able to differentiate the objects sent to it.


The way my data is converted into a draw call buffer is in the graphics function,where i pass in my rotation and position to the cMatrixTransformation constructor to create a 4x4 matrix.

I feel this is not ideal and I would want to maintain a drawable class that has the data required for the drawcall.This drawable data is created in the submitMesh function.



Game code that submits a drawcall

```
	eae6320::Application::cbApplication::sendToGraphics(square);
	
	eae6320::Application::cbApplication::sendToGraphics(floor);
	
	eae6320::Application::cbApplication::sendToGraphics(mainCamera); ```


As mentioned above the Gameplay programmer considers the camera just like anything else he deals with interms of graphics and just submits it.I dont have the functionality right now for multiple cameras.I think this is convinient for the gameplay programmer.




