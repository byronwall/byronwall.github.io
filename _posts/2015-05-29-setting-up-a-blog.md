---
layout: post
title: Setting up this blog
category: blog
---

This post contains a little bit of info about how I got this Jekyll blog setup.  It's your standard first post...

Fork a copy of Skinny Bones.  Fortunately, this is bare bones enough that GitHub can build it outright.

Add a little bit of starter info to the `\_config.yml` file. **Don't accidentally leave out the space between the `:` in the key-value pairs**

Cloned a copy of the repository to a local directory to avoid creating everything in the web interface.  Using GitHub for Windows saves a lot of hassle over the other interfaces available.

Created a posts folder with a blog subfolder.  Do not create the subfolders for this.  Instead use the `cateogry` tag inside the front matter to create the permalink to _look_ like a subfolder.

Moved an image over for the teaser.  Link here does not need to include `/images/`, just the file name.

**Updates 7/13/2015**

Converted over the minimal mistakes Jekyll theme.  It looks much better for a portfolio style site with the bio details on every page by default.

Tried to use collections in order to keep the Projects separate from the Posts.  This did not work very well.  Maybe at some point I will come back and make this work.  For now, they are set by a category and kept separate using Liquid.
