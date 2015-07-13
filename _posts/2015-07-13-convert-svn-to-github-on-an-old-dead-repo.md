---
published: true
title: "convert SVN to GitHub on an old, dead repo"
layout: post
category: blog
---


The recent goal has been to move as much source code over to GitHub as possible.  For more recent code, I was using Git anyways, so it was simple.  For older code, I was previosuly using Subversion with locally hosted repos.  It's been years since the server was running so the question was: how to get these repos over to GitHub?  Fortunately, I keep all the original repo folders on an old drive and was able to copy them over to a newer drive for processing.

There are two ways that I ended up doing it.  The second was far easier than the first:

##Round 1: `git svn clone` and some other steps

The first approach followed the steps in [this write-up](http://john.albin.net/git/convert-subversion-to-git).  Overall, they worked as advertised.  In order to get a good URL for the `git svn clone` step, I started up an instance of `svnserve` to use `svn://localhost/` URL instead of `file:///`.  The `file:///` version gave an error about formats not matching.  See this [SO question](http://stackoverflow.com/questions/5113170/git-svn-is-unable-to-fetch-from-svn-repository) if you want the details.

##Round 2: let GitHub take care of it

The second approach was using the import feature on GitHub.  In order to get this going, I needed to expose `svnserve` to the outside world.  After repurposing `home.byroni.us` for this cause, I was able to get GitHub to recognize the repo.  Note that to make this work I used `svn://home.byroni.us:3690`.  It did not work with `http://` at the front.

This approach is much easier because it allows you to redfine the authors while it processes the repo instead of going through a text file.

For the cost of exposing `svnserve` to the outside world, this second approach was far prefered.  It handled a much larger repo faster than the other method.
