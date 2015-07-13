---
layout: post
published: true
title: C# Projects
category: project
---

##Summary
Most of my C# work has been done on the side to solve small and interesting problems, general utility helpers at work, and one or two serious programs.

##Process Data Gatherer to Replace FTP
In my first internship, I built a C# program to gather process historian data to replace an old school mainframe request and FTP system.  The program was built to look at archive files stored on the intranet (backups of historian data) and process then to yield the desired data.  Information was stored per tag and read from the raw storage format.  This required a fairly nasty conversion from one style of float storage to modern day float storage.  Once the data was pulled into the program it was plotted using Microsoft Charts. There was also an option to export the data to Excel via Interop with some of the formatting and analysis handled on the transfer.

##last.fm scrobbler
This was a side project built mostly to experiment with WPF.  It dialed in to the iTunes event library and tracked songs that were playing and scrobbled them at the half way point.  The program also made requests to last.fm to provide some data and context about the currently playing song (related artists mostly).  Other features included:

 - queue and historical log so that offline scrobbles could be made after the fact
 - program had an updater that could run alongside and pull down fresh updates
 - maintained its own database of songs that were played and provided some analytics of that data (this never got as far as I hoped)
 - made extensive use of templates and data binding to get a web like interface

##block game solver via genetic algorithm
There is a game out there that I always loved to play.  It still exists in some version: touch a colored group of blocks and they disappear.  The surrounding blocks fall vertically and usually close horizontal gaps when a column is cleared. Rinse and repeat until the board is clear or only single colors remain.  I also used to think I was good at this game until I built this program which could find near optimal solutions using genetic algorithms.  This program will get revitalized and ported over to a web solution so that I can do some interesting d3 visualizations with it.

##Excel Interop work
With a strong background in Excel / VBA programming, it is fairly natural to also tend to use the Excel Interop libraries when the chance arises.  Most recently, I have just been using that knowledge to answer questions on Stack Overflow, but I have also written real code in this realm.  The most recent example was a helper tool at the plant which processed scraped some HTML and sent the data to Excel.  It was the basis for a visualization helper in Excel.  The HTML probably could have been scraped from VBA, but I never thought of it at the time.

##countless utilities
Barely worth mentioning all of the utility code that has been written over the years (but I will):

 - file watching programs to track changes on networked locations
 - `Timer` based programs to do who knows what at this point (I used to love putting these in the system tray to just check things)
 - Microsoft Charting related programs (I was fairly active for a while on the MS forum answering those questions)
 - handful of programs to open multiple webpages or process webpages in a work setting where applications did not want to be RESTful
