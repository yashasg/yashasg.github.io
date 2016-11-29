---
layout: post
title: Game Graphics-Assignment 12.0
published: true
---

#Mesh Textures.
<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment13/gamess.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~10 Hours.
[Download-Assignment 13.0](http://cade.utah.edu/~gujjar/Assignment13/game.zip)


_Purpose of the Assignment_:

Purpose of the Assignment was to enable UV mapping on our meshes so we can use textures to set color for every pixel

_How I did the Assignment_:

I think this assignment was fairly easy,but one thing that was a suspense was that you dont know if you are doing everything right,until you see the final texture on the screen.So i just hoped that my planning was right,otherwise a ton of work would have been wasted,but it all worked out well in the end.

_My First Task_:
I went in an found a mesh with a texture,because my player ship didnt have a texture on it,only colors.I was trying to open the model in maya and wrap my uv image to my texture,but it was just not working,I eventually gave up, hoping it was my lack of maya knowledge and hoping it could make it work in my engine.


_My Second Task_:
I imported all the different project and file changes I needed to for the assignment and set the dependencies.This was fairly easy, been doing this since the first assignment. In the same task i then set my TextureBuilder as the startup project and gave it the default texture to build,it worked just fine and gave me confidence that I can use it with build all assets.


_My Third Task_:
Changing shaders is something I feel I am unfamiliar with, I intend to change this in the future, But anyway, I went in and added texture coordinates to the vertex shader and the fragment shader, I didnt do the platform independent shader file,so I had to change it in 2 places, If i have to keep making more shader changes I will reconsider making it platform independent,but for now I am ok with making changes in 2 places.Another thing that I did was make changes to the mayamesh exporter so I could export UV data.

A sanity check was to make sure the game still worked after adding all this changes,and turns out it did,One small change I made was that in my sVerrtex.h struct,I was forward declaring the color struct and the UV struct,but I realised there was no point in doing so, I dont intend to use the color struct and UV struct outside of the Vertex,so why should my API expose that header,so I just made the color struct and uv struct local to the vertex.h file,avoiding forward declarations and confusion with Graphics library exposing things it doesnt need to.
_My Fourth Task_:
I added the texture path to the material and this is what my material looks like right now

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment13/materialss.PNG" frameborder="0" allowfullscreen></iframe>
If i had to add more than 1 texture for my mesh I would actually put it in a Lua table,something like this
```
Textures={
"Some/Path",
"Some/OtherPath",
}
```

Looks clean right?

But wen we create a binary file,I place the constant material data in first,so when I am traversing it I can offset the pointer correctly to the start of the effect path,and that's how I did it the last time,but now I have 2 paths with variable length,so while building,before the effect path I added the length of the path,so during runtime when I am traversing,I add the length to the offset to get the next string immediately,And if I had another texture path then I would put the length of the first texture path before the texture path, the whole point of binary file is to make runtime faster, and this helps because I dont have to traverse thru the string to find the null character,get the length and stuff. Its so fast, it should be in the next Fast and Furious movies,replacing Paul Walker. :). 

This is how it looks in binary

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment13/binmatss.PNG" frameborder="0" allowfullscreen></iframe>

This is how i traverse through it in runtime

<iframe width="700" height="700" src="http://cade.utah.edu/~gujjar/Assignment13/cppmatdata.PNG" frameborder="0" allowfullscreen></iframe>

As you can see after reading the constant material data,I go in and read the length of the effect path,which i use 8 bits to denote(so in unsigned int the range is between 0 to 255 characters) and once I have that I offset the existing pointer with a byte and point my effectpath pointer to the next data,then I added the length previously extracted from the file and add it to the offset to get the starting pointer to texture path,which i use my texture path pointer and update.

I wasn't kidding about Fast and Furious. :P
	
State of the Final Game:
I have added a little visual sugar to the game,when the player moves from left to right the ship rotates a little to make it seem like it is moving,and I also added a background png to the game and my player has a cool mesh and texture I found online. I am having some trouble with shader stuff,but thats not hidering my assignment,so Ill work on it when I have the time.
Controls
Player
W to move up

A to move left

S to move down

D to move right.

Space to shoot

The bullet,player and camera also moves independent of frame rate.The way I did this was to multiply the offset of the movement with time taken during previous frame.






