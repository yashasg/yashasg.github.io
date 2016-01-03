---
layout: post
title: Neo Tempest
published: true
---


##An Endless Arcade Warp Runner,based off the legendary arcade game "Tempest".Includes a cool level-building feature.
<iframe width="640" height="315" src="https://www.youtube.com/embed/Hope4KOhNvM" frameborder="0" allowfullscreen></iframe>

[Project Link](https://drive.google.com/open?id=0BzP8IKIJhlC7ZTFObXVWZEI2bEk "Motor Mania-Top down,demolition Derby")

[Download-Neo Tempest](https://drive.google.com/open?id=0Bwk0Q_HJWPA4Z0Q1bWhFMkpHYXM)

**Post-Mortem**

_1st Week_:The first week was pretty much discussing different ideas for an arcade game, and
learning JavaScript. My co engineer was a little familiar with Javascript so he started working on
the game with place holder assets. I feel that we hurried into the development stage, as the
library we picked for the game development, PIXI.js was very limited compared to other engines
that other teams used. We as engineers did not have a discussion on the framework to be used,
so I had to just accept PIXI.js and start exploring into it. We divided work where I decided on
making the level builder for the game and the algorithm for the opponents. By the end of first
week we had a working prototype with a plane moving in a circle, we had a level builder which
only worked on firefox.
_2nd Week_:Setting up Opponents algorithm‐I took on the task of writing the algorithm for the
opponents. In the game Neo Tempest the opponents are just textures being scaled from the size
of 0.2 to 1, the scaling makes them look like they are moving closer to the player. My algorithm
was perfect for opponents but fell flat for the obstacles, mostly because the opponents were 2d
images while and obstacles had a 3D feel to it. It was a challenge to scale the opponents
correctly and also keep them in the tube(which is the play area of the game),which I did fairly
well. I also worked on creating the start screen for the game, which was greatly appreciated by
the team.
_3rd week_:This was the crunch week, all the stuff me and Sid(co engineer) worked on over the
past 2 weeks had to be integrated into the game, which ended up in a lot of issues. The level
builder that I made needed a Wamp server which hosted a PHP file containing the level Data, Sid
decided to take another route and implement the same using python server which was also a
slightly better option, which I was not aware of. But it was a learning experience. I later worked
on an end state for the game and a restart state for the game, which was fairly easy but took a
lot of time, because I had to traverse through unfamiliar code and make changes to it without
breaking it.
