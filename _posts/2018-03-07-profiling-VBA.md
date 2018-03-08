---
layout: post
category: blog
published: true
title: Profiling Excel VBA
---
If you find yourself wanting to profile VBA code from Excel, your options are limited.  There are currently a number of apporaches out there, but none are truly as easy as you want.  The main problem is simple enough: VBA does not provide the necessary hooks to just add a profiler without touching your own code.  This means that you are required to modify your own code to add a profiler.  This means that unless you _really_ need to profile your code, you will likley avoid the burdern.  To make this process a little eaiser, I built a quick tool to automatically add profiling code ot an existing VBA proejct. The biggest feature here is that the code will run without additioal references or any extra code withing your project.  It works by parsing your code and adding a number of `Application.Run` commands which call out to the same spot that gneerates the code.  That means: if you are able to load the addin which can add the prfilign code, you can already support the profiling.  There is a ismple interface to add code to a specifc module.  From there, you run your code like nromaly, and the addin will take care of tracking the calls.  The addin handles the task of automatically tracking the call stack and adding adn removing groups.  Once your code has run, you hit a keyboard shortcut and the results are opened in a new workbook.

Link: add to bUTL

Other sections to add:
* How it works
* Why it was made
* How it will be improved
* Any prior art it was built on

TODO: add some images of operation