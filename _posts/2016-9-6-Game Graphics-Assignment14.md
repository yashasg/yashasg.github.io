---
layout: post
title: Game Graphics-Assignment 14.0
published: true
---

#Mesh Textures.
<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment13/gamess.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 14.0](http://cade.utah.edu/~gujjar/Assignment14/game.zip)


_Purpose of the Assignment_:

Purpose of the Assignment was to setup a way to display 2d sprites for our game.

_How I did the Assignment_:

I started this assignment really late because I had had a ton of work from Gapp lab this weekend, I feel guilty for spending such little time on it,but it works :).

_My First Task_:
I found a sprite of a heart that I wanted to display as the players health on screen,that was my first step towards this assignment. I also went in and added the required files to the solution,and then spent some time getting rid of the errors on them.


_My Second Task_:
Adding render state to my code first,for this I had to understand how the cRenderstate and the renderstatebits logic works,and i must say its pretty interesting. Just to give a background on it,the render state tells the graphics engine what kind of object is being rendered,if it is a mesh there are a different set of parameters for the render state as compared to when the object is a UI object.The parameters are essentially AlphaTransperency,EnableDepthBuffering and DrawBothSidesOfTriangle.The names are self explanatory,Our meshes use the order of false,true, false for the above values respectively.And for Ui objects the order is true false true.

This is how my normal effect file for meshes looks like


<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment14/effectlua.JPG" frameborder="0" allowfullscreen></iframe>

Lets take about how I represent them in binary,like I mentioned before,bool is expensive on memory,and writing out each bit is fairly cheaper,but that is still 3 bytes on the file representing 0 or 1.There is a better solution,our old friend uint8_t datatype.we just make a variable and assign the bits to the variable lets say we want the render state for a mesh, to represent the Alpha transperency we just add the bit 1 and left shift the value 0 times,for depth buffering we left shift it 1 time and for DrawBothSides we left shift the value 2 times, so if we have all the 3 enabled the bits in the uint8_t pointer will be
0 0 0 0 0 1 1 1  which will have a value of 7.

If you are thinking,oh but during runtime we have to do some amount of computation to retrive the actual bits from the value, I had the same question,but a computer is the fastest when working with bits, and specifically the bitwise & operator is our friend in this process.

Anyway this is how my file looks in binary

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment14/effectbin.JPG" frameborder="0" allowfullscreen></iframe>

I think storing bitwise data in a byte is the most efficient way of solving data and computation problems.




_My Third Task_:
So before doing the above I just hardcoded the default renderstate value and tried to see if my meshes were still rendering.This helped me make sure that I havent messed up until now.

_My Fourth Task_:
I need to bring some history in this,I had a shader problem that only the last shader I loaded was being used by the GPU,I figured out the problem,in my need for speed(performance) I thought, the effect.h files dont need to maintain VertexShader,PixelShader and InputLayout pointers as memeber variables,ill just make static version of them and use them,the past me didnt have any idea how wrong I was.As expected,everytime the effect load was called the static functions were getting udated with the new shader data and thats why only the last loaded Shader was being displayed.Kun Cheng an awesome Engineer helped me figure it out.

_My Fifth Task_:
After this the rest of it was fairly smooth,I created a struct encapsulation for Ui stuff,called them UiObject.The cSprite and material are pointer types in my UiObject struct.I also added a new overloaded SubmitToGraphics function that takes in a UiObject and all that good stuff.

Some Questions Answered

This is how my texture looks when the resolution is square 640x640
<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment14/spritescreen.JPG" frameborder="0" allowfullscreen></iframe>

This is how my texture looks when the resolution is square 1080x640
<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment14/spritescreenstretch.JPG" frameborder="0" allowfullscreen></iframe>

if you noticed the Ui object looks stretched,it is because I set a top left top right bottom left and bottom right positions fixed in my code,that means that when the screen stretches my positions also stretch with them,making it look a little blurry.


State of the Final Game:
The Ui object adds a nice visual health bar to my game so thats a good thing.
Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






