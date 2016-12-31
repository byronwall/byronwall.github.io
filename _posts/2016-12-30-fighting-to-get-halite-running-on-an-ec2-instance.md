---
layout: post
category: blog
published: false
title: Fighting to get Halite running on an EC2 instance
---
I have been looking for an excuse to finally try out EC2.  I figured while testing Halite bots, I may as well let some poor computer in the cloud deal with the CPU cycles instead of my lap under the MBP.  Several hours later and I got the bots to fight in the cloud.  It was nothing short of a fight to get there.  Full disclouse: this was my first real foray into using Linux, SSH, SCP, remote connections, and most everything else required to get this going.

The ~~high~~lowlights follow:

First, do not use an Amazon Linux instance to try and do this process.  Turns out the Halite bot executable depends on the JSON in C++ library which cannot be built with GCC 4.8.  Also turns out that you cannot install (easily?) install anything above 4.8.3 using the Amazon Linux instance.  It may have been possible to download the source for GCC and get a version above what was available, but that was a road I did not want to follow.  It were any other program the compiler, I would not shy away from the source, but I feared that compiling the compiler would be turtles all the way down.

Getting to the point of knowing that Amazon Linux was not going to work was obviously not the first step in the process.  The actual first steps were:
 * cull together the files I wanted to move over to the EC2 instance (put them in a folder called xfer), easy enough
 * figure out the SCP command that is required to move those files over to the EC2 instance
 
 for future reference `scp -i bot-tester.pem -r ~/Projects/halite/xfer/ ubuntu@ec2-35-165-254-16.us-west-2.compute.amazonaws.com:~/.`
 
 * figure out the SSH command to see if those files actually got over there.  Fortunately, Amazon gives you this one.
 
 for reference `ssh -i "bot-tester.pem" ubuntu@ec2-35-165-254-16.us-west-2.compute.amazonaws.com`

Instead of the Amazon Linux instance, fire up an Ubuntu one instead.  Once I had that sucker responding 
