---
published: true
title: Kaggle and R Projects
layout: post
category: project
---

## Kaggle Contests
I have competed in a couple of Kaggle contests in order to learn R and work on real world data sets.  I entered both the Telemetry challenge and also the Otto Classification challenge.  In both of these projects, I learned a great deal about how to properly use R and document work.  It is easy in a exploratory setting to make a mess of a workspace.  I am currently applying those techniques to 2 ongoing Kaggle contests and will post code when they are completed.

## Telemetry challenge
This was a contest where the goal was to determine if a given set of telemetric data belonged to a driver in question.  The idea was that given 200 routes of a "single" driver, you were to determine which of those 200 were not actually driven by the driver stated.  I tackled this problem with a bit of the knowledge I gained mapping routes from runnDAILY.  I was able to apply a number of vector based translations in order to normalize the routes.  From there I implemented a script that could determine how similar a set of routes were based on the delta between points in the route.  The deltas were used to feed a hierarchical cluster using single linkage to determine which ones belonged to the same group.

I had a good time working on this project.  The only downside was the size of the data did not mesh well with a first project and learning R.  It took several hours on my hardware to process the entire data set which made it difficult to test and rerun.  In the future, I will doing the heavy lifting with AWS.

[Kaggle page for the contest](https://www.kaggle.com/c/axa-driver-telematics-analysis)
[Code and efforts at GitHub](https://github.com/byronwall/Kaggle-AXA-contest)

## Otto product challenege
This was a Kaggle challenge that was focused on classification of a number of different products into 9 overall categories given a large table of information about each item.  My work on this was limited to implementing a neural net based classifier with no attempts at optimization.  I did not have the free time I expected to dig in to this contest.  I did a bit of work visualizing the data set using R and ggplot2.

[Kaggle page for the contest](https://www.kaggle.com/c/otto-group-product-classification-challenge)
[Code and efforts at GitHub](https://github.com/byronwall/Kaggle-Otto-Product)
