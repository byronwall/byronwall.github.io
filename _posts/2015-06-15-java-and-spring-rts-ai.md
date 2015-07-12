---
published: true
title: Java and Spring RTS AI
layout: post
category: blog
---


## Spring RTS AI
I grew up loving to play Total Annihilation and was always awed at how people created AIs for RTS games.  When I noticed Spring, my first thought was: when will I extend this to create my own AI.

I finally took the plunge several months ago, reading a book on AI and learning enough Java to cobble together a working AI.  The AI exists and will play a game, but it's not particularly effective... yet (isn't that the pitch for every side project AI?).

Current feautres of the AI include:

 - Good plumping to allow for timed events and behind the scenes of updating internal models.
 - Decent understanding of the tech ladder for Balanced Annihilation which ensures a progression to more advanced units


What's left to be done:

 - Everything else?
 - Improve the task selection scheme so that different goals are given correct weights
 - Improve the location related tasks, specifically where to group and attack and where to build new structures
 - Improve the responsiveness aspects of the AI which would allow it to rethink an action if attacked or help out a buddy if they are attacked.  This could also apply to the construction units as well
 - Get beat by the AI... that's really the main goal: to make somethign I actually want to play against
