---
layout: post
category: blog
published: false
title: Fighting to get Halite running on an EC2 instance
---
I have been looking for an excuse to finally try out EC2.  I figured while testing Halite bots, I may as well let some poor computer in the cloud deal with the CPU cycles instead of the MBP on my lap.  Several hours later and I've got bots fighting in the cloud.  And turns out that the newest version of the bot is decent.  It was nothing short of a fight to get there though.  

Full disclouse: this was my first real foray into using Linux, SSH, SCP, remote connections, and most everything else required to get this going.  What follows is what happens when you approach a mildly complicated problem with that base level of understanding.

### What not to do ###

First, do not use an Amazon Linux instance to do this.  Turns out the Halite bot executable depends on a JSON in C++ library which cannot be built with GCC 4.8.  Also turns out that you cannot install (easily?) anything above 4.8.3 using the packages available in the Amazon Linux instance.  It may have been possible to download the source for GCC and get a version above what was available, but that was a road I did not want to follow.  I feared that compiling the compiler would be turtles all the way down.

Getting to the point of knowing that was obviously not the first step in the process.  The actual steps were:
 * Cull together the files I wanted to move over to the EC2 instance (put them in a folder called xfer), easy enough
 * Figure out the SCP command that is required to move those files over to the EC2 instance. For future reference.  (This is actually the ubuntu one from later, the original used `ec2-user` as the user) 
 `scp -i bot-tester.pem -r ~/Projects/halite/xfer/ 
 ubuntu@ec2-35-165-254-16.us-west-2.compute.amazonaws.com:~/.` 
 * Figure out the SSH command to see if those files actually got over there.  Fortunately, Amazon gives you this one. For reference 
 `ssh -i "bot-tester.pem" ubuntu@ec2-35-165-254-16.us-west-2.compute.amazonaws.com` 
 * At this point, things get a bit specific to actual task of running Halite games on the server, but the mile-high view is that I needed to get a Python3 script going called `manager.py`.  You can find [that over on GitHub](https://github.com/smiley1983/halite-match-manager) if you're interested. 
 * Checking to see what version of Python was available... 2.7... no dice. Checking to see how to install Python3... `sudo yum list | grep python` reveals python-35 as an option... `sudo yum install python-35` and we're off.  Not really, that `manager.py` also needs the `skills` package installed.  A simple `pip3 install skills`?  Definitely not.  Back to the yum list to see what's on the menu.  Find the right package, figure out the alias, and then we're off and running with the `skills` package.   
 * Again, not really, it's at this point I realize I forgot to bring over the binary for halite.  No fear, there is a simple `install.sh` script hosted on their GitHub.  And it is at this point that I realize why you cannot use the Amazon Linux instance.  The version of [GCC available is not supported by the JSON library](https://github.com/nlohmann/json#supported-compilers) that the folks at Halite are using.  There was a short period of trying to upgrade the GCC version before I terminated the instance and tried again.

### Round 2, use an ubuntu server instead ###

Instead of the Amazon Linux instance, fire up an Ubuntu one instead.  Once I had that sucker responding, I was able to repeat the steps above.  Forutnately this time, Python3 was installed by default.  The steps from that point:
 * Try to get the `install.sh` script to run.  This time the first issue was on `unzip` not existing.  A quick `sudo yum install unzip`?  Of course not, new Linux, new package manager.  This one I actually knew though from seeing enough XKCD comics `sudo apt-get install unzip`.  Since I knew it was coming, I threw in another one to get `gcc` and `g++` (versions >5 to avoid the JSON debacle).  There was one last error about `make` not existing. Installed that, and now we're off, we've actually got the binary compiled and ready to go.
 * Somewhere in there I had to create a symbolic link to `gcc++-5` from `gcc` in order to get `make` to work.
 * At this point, I've got a working halite binary and can run the `runGame.sh` script and actually get a game to play.  Look at that!  I got the bots to play in the cloud.
 * The final piece was to use the actual game manager that started this whole thing.  I pop into that directory and run the command to play some games `manager.py -m`... and... a call stack dump related to parsing an integer!  This one actually threw me for a loop since the same file works fine on my local machine.
 * Needing to see what happened on that results parsing step, I figured I'd do the usual throw in a `print()` call and see what the computer saw.  Except... how do you edit a text file from an SSH terminal?  Is there where VIM comes in?  Do I actually get to use VIM for real?
 * Here we go, let's edit that text file. `vim manager.py`.  Issue is at line 119 or so.  Apparently `:` is the magic key to control things. `:119<CR>`.  Boom, looking at the spot now.  Need to insert some text.  A quick trip to StackOverflow reveals that `i` is the key to do that on OSX.  Throw in my `print(self.result_string)` and save the file `<ESC> :wq<CR>`... and... get some very sensible output from the halite run.  For some reason it's expecting to see player info a line early... what gives?  I run the same command on my local machine and see that a line is missing from the output??! Turns out the folks at Halite updated to version 1.1 and added that line of output.  Not sure why they put it smack dab in the middle of previous output, but whatever.
 * Back to VIM to edit some line numbers and get the output to match the parser.  Exit out of there and hit it with the magic `manager.py -m` and it works!!!
 
 At this point I've got my bots playing the cloud and I don't have to deal with the heat generated by their inefficient searches and poor strategy.  Assuming I can milk this free tier of EC2 for all it's worth, I'm set for the length of the Haite competition.
 
 The bulk of this process would have been significantly less painful had I known something about EC2, Linux, SSH, SCP, or the trivial ins and outs of package naming and installation on different Linux distros.  Of course, that's the whole point to these exercises.  Need to deal with the pain of this process sooner or later.
