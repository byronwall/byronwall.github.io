---
layout: post
category: blog
published: true
title: Commute viewer
---

*This is a work in progress, will finalize soon enough... just hit send though*

## commute viewer

I created a tool to help visualize the range of commute times.  I will soon be moving to Indianapolis for a new job and wanted to know possible commute times from different areas of town.  Google Maps does a decent job of providing this information if you ask to `Arrive By` a certain destination at a certain time on a certain day.  The "decent" part is the fact that they only give a range of possible times and do not give a sense of the distribution of times.

To provide a little better visualization of the possible commute times, I created a tool which would load up the various commutes and take screenshots.  Those screenshots were then stitched together into a movie to provide the full picture of how the commute developed throughout the morning and evening rush hours.

To accomplish the description above, you could simply open a browser page with the various commutes loaded and refresh the page every 10 minutes.  For the first pass at this, that's exactly what I did.  After one day of doing that however, I realized this was a good chance to use a headless browser and automate the task.

The full project is on Github (TODO: add link) and provides a description of how to use the tool.

On this site however, I'll point out a couple of observations from the experience and how I would handle a similar task in the future.

The headless Chromium experience was quite painless using `puppeteer`.  I cheated a bit since I was not concerned about time taken and delayed the screenshot by 5 seconds.  I initially attempted to use the `no network activity` events, but those always seemed to catch the map in a partially loaded state.  The only other headache here was dealing with the `async/await` code samples from `puppeteer`.  I wanted to reuse the `puppeteer` instance but couldn't quickly figure out the syntax around the `await` calls so I just fired up a fresh instance for each link to follow. I probably should have switched to Promises.  For a more serious task, I could probably not get away with firing up a new instance each time.

For the movie making experience, my goal was to avoid creating a ton of temporary files on my hard drive with the intermediate results.  There was an intermediate result because I wanted the clock time of the screenshot overlaid onto the image.  This process introduced a huge mess of converting between streams and buffers and callbacks and Promises in order to get the libraries to work together (also I'm on Windows).  This all came together but the final mess is definitely hacked together.  The real issue with all of this is that by default, the various pieces of the program will shoot off to completion and wait for callbacks if allowed.  This then creates a problem where 30+ ffmpeg instances all fire up at the same time.  I used Promises to enforce a sequential action here, but the final result was not particularly elegant.

In general, this tactic of loading up a headless Chromium instance to save snapshot of a webpage worked great.  The screenshot looked exactly as I expected.  There was a slight trial and error on the zoom level and map centering, but that was easy enough.  For a "normal" web page that is not a scrollable map, I assume this step falls off since you just visit a single URL.

Finally, I am fully aware that Google Maps has an API that would have provided the commute times in a single request (I used this API extensively for runnDAILY).  I was really interested in obtaining the full traffic coloration the way it normally looks in Google Maps.  I did not want to trudge through the API docs to see if I could quickly replicate those colors using one of their lines.  I was also looking for an excuse to try out a headless browser, so I was biased on implementation going into the thing.

Future efforts to consider:

- Parse out the travel time and preferred route from the image (at this point, I should really use the API instead of scraping those details)
- Provide some overlay across multiple days to show common traffic bad spots.  Right now this process ends with a video for each unique combination of commute, day, and morning/evening.  The videos are easy to process visually but do not help with bulk analysis.
