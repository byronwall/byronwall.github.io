---
published: true
title: Java Project, Spring RTS AI
layout: post
category: project
---

Java is the first language I learned, and I have come back to it recently to build an AI for the Spring RTS platform.

##Spring RTS AI
[**Source on GitHub**](https://github.com/byronwall/SpringBot)

I grew up loving to play Total Annihilation and was always awed at how people created AIs for RTS games.  When I noticed Spring, my first thought was: when will I extend this to create my own AI.

I finally took the plunge several months ago, reading a book on AI and relearning enough Java to put together a working AI.  The AI will play a game, but it's not particularly effective... yet (isn't that the pitch for every side project AI?).

Current features of the AI include:

 - Good plumping to allow for timed events and behind the scenes of updating internal models.
 - Decent understanding of the tech ladder for Balanced Annihilation which ensures a progression to more advanced units

What's left to be done:

 - Everything else?
 - Improve the task selection scheme so that different goals are given correct weights
 - Improve the location related tasks, specifically where to group, attack, and build new structures
 - Improve the context awareness of the AI, allowing it to rethink an action if attacked or help out a buddy if they are attacked
 - Get beat by it... that's the real goal: make an AI I actually want to play against
