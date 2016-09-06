---
layout: post
title: Game Graphics-Assignment 2.0
published: true
---


##Animated square woohoo!!.
<iframe width="640" height="315" src="https://www.cade.utah.edu/~gujjar/Assignment2/square.PNG" frameborder="0" allowfullscreen></iframe>

Time Spent: ~12 Hours.
[Download-Assignment 2.0](https://www.cade.utah.edu/~gujjar/Assignment2/game_9_6_2016.zip)


_Purpose of the Assignment_:

The Purpose of the Assignment was for us to setting up the Lua project and also some of the functions used to communicate data between Lua and c++ code.But this assignment turned out more towards checking if the dependencies are right 

_How I did the Assignment_:

_Just like last time,I broke down my Assignment into tasks_.

_My First task_:

was to read through the assignment page and its links to other pages, which took quite a lot of time, Especially, this time, I felt the reading because very vague and important information was hidden between lots of words.Though the amount of reading was less, this time,I felt like I didn't know enough when I got into making changes to the project.

_My Second Task_:

I started setting up my main solution by adding the files provided by JP.I first replaced all the projects that needed to be changed,namely the AssetBuildSystem and the UserSetting project.There were also 2 new projects I added,which were LuaExe and the Lua static library.Luckily, the property sheets were already added to the changed projects. In this task, I also set the dependencies for the projects, so to avoid future linker errors.The LuaExe, AssetBuildSystem and UserSettings now depend on the Lua static library.

_My Third Task_:

This was the task that involved getting down and dirty with the c++ code.There were some methods that were well defined and had a level of error checking in them,which I used as a coding reference to complete other methods.The first thing I did was replace the EAE6320TODO with a //TODO so the TODO lists show up in the task lists window.This is quite a useful way of organizing the things we want to do in our code.During this task, I made a mistake of commenting out important c++ function called through Lua,and because the error handling for such issue is minimal,I kept getting a message that return of the function was null, but actually the function was never even being called in c++ because it was commented out.This took me some time to figure out.Geeting more technical with code,the comments said I was supposed to return things in c++,my basic understanding was to use the return statement in c++,and I didn't know how Lua could find the return value.Going back tot he usingLua example I saw that returning something  back to Lua is about pushing it back to the stacks so that Lua receives it.What we do end up writing in the c++ return statement is the number of values we returned to Lua.For example,if the function was to return a boolean and an int,we first push them to the Lua stack and then the ReturnValueCount is 2.

So I made all the changes and cleared up the TODO list pretty soon. It was time to see these things in action.

_My Fourth Task_:
With a few more brief changes, I was able to see the triangle rendered in Assignment1. This was relieving knowing that the hardest part of the assignment was done.And it was actually easier than I thought.I built on all platforms and configurations just to make sure everything works fine with Lua.And it did,no problem.

_My Fifth Task_:

Increasing the size of the vertex buffer

This was actually intuitive enough and just involving the triangle count to be increased.The tricky part was to render the triangles using the handedness logic. I just referenced the logic in which existing vertices were placed for that platform.and then followed the same rule for the new vertices.But as a rule of thumb this is how I remember the handedness using an opposites logic , directX has an R so it renders Lefthanded triangles,and opengL has an L so it renders Righthanded triangles.
A small issue I had with the code setup is that the TriangleCount variable is being set twice in the code,so we need to change it in 2 places for the square to be drawn.

_My Sixth Task_:

_UserSettings_:

The  project is now supposed to log the resolution in which the project was supposed to be built. This seemed like a complicated task because it involved going through the UserSettings.cpp file to find out where exactly the project was logging the resolution width and height.Turns out the log comes from application project and not UserSettings,but as the requirement was to set it up in user project,I used the s_resolutionHeight and width variables and used the OutputMessage() method for logging them.

These are the 2 lines I write in my log

```The user settings file has the Width: 640

The user settings file has the Height: 480```

These change every time the file settings file is updated and the game is run.So basically it logs the user settings in the last run of the game.It makes sense for it to update this was,so if there is an error due to a usersetting,the log is the only thing the developers will need to replicate the same scenario in their system.

I also noticed that if the settings.ini file is updated in the solution folder,the updated setting doesn't get deployed to the new location.This also makes sense because if there is a patch that is deployed they publisher doesn't know the users preferred settings and overriding the settings of the player with the published settings may frustrate the player.

_My Final Task_:

_Still work in Progress_:

Ajinkya showed me that rebuilding the whole solution actually caused the build to fail,the second time we rebuilt the solution.I am still trying to figure out why this is happening.A quick way for fix this was to unload the LuaExe project,but this didn't seem like the right answer for the problem so I didn't do it.


