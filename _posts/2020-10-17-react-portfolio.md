---
layout: post
category: project
published: true
title: React Portfolio
---

I have been using React for the last 4 years for side projects and at work. This page summarizes all of the projects I've built using React. Over the last 4 years, I have progressed significantly in building React apps. My two "flagship" projects were built in the last 2 years working at Allison Transmission. Those include a data analysis platform and an interactive hydraulic schematic tool. Unfortunately, I can only describe those projects. Other projects for personal interests include an offline Hacker News reader, a family recipe and cooking site, and an RSS reader for news sites.

My typical setup:

- Use TypeScript exclusively now
- Server typically done with Node.JS
- React Component classes (instead of functional components). I've found these much easier to use with TypeScript. I also don't mind the verbosity.
- Blueprint.js for standard UI/UX Components
- Lodash for standard utility functions
- d3.js for data visualization

## HN Offline (2018 - 2020)

This is a simple web app to read Hacker News comments by storing a local copy. App uses service workers and local storage to provide fully offline HN reading. The goal of this app is to read the comments. It does not provide an offline version of any articles or non-HN links.

### Features

- Optimized for lurking. No ability to login, comment, or do anything other than read comments and follow links.
- Three main views for accessing stories: front page, day, and week. Each view provides 50 stories. Infinite scroll is intentionally avoided.
  - When loading a list of stories, _all_ comments are loaded for _all_ stories. Experience says loading all 3 pages will require around 15MB of local storage.
- App locally stores HN pages that have been visited to grey them out on the main page.
- No logging, analytics or other tracking on the server.
- Optimized for mobile including `code` blocks which normally look awful.
- Any links to other HN articles are automatically loaded in the app.
- While reading comment threads, a pleasant UX is provided to:
  - Click to collapse a thread and its children. A clickable margin is provided for each parent level on every child.
  - Click the right margin of the comment to make deeply nested comments wider.
  - Comment collapse state is stored in the current session.
    - If you leave a story and come back the comments will return to their previous state.

### How It Works

This is a simple web app. Server is built on Node and Express. There are two APIs which are consumed:

- Official HN API, via Firebase - used to load front page list, story, and comment details
- Algolia HN search results - for the top day and week stories

The server has a simple timer which triggers every 10 minutes to check for updates for the front page. The day and week lists update less frequently. There's additional logic to only reload the comments for a story if enough time has elapsed from the previous update.

The client is a SPA built in React. The bulk of the code is data management and controlling the view when comments are collapsed.

Built in Typescript.

![Mobile screenshot](mobile.png)

## Family Recipe and Cooking App (2020)

TODO: create a README for this project and then copy over here

## YouTube Recommender (2018)

This is a quick server which is used to make better YouTube playlists. It uses a combination of your Watch Later, Watch History, and the YouTube API to provide better playlists.

The goal of this project was to make it easier to select good content from a Watch Later playlist that had more than 500 items. I was using that playlist as a dumping ground for things that might be good. The approach was simple: use the positivity ratio (thumbs up / down) to weight the view count. This gave a nice balance of highly positive content with low view counts and moderately good content that was heavily viewed. When building a playlist it also only allowed a single video per channel at a time. This prevented a single popular channel from dominating.

Overall, it built very nice playlists which could then be picked through more easily.

The client was just a simple interface for creating the playlists. The hardest part of all of this was accessing the watch later playlist. Unfortunately, YouTube does not let you access this playlist for a user (even if authenticated). To get around that, I created a simple bookmarklet which could process the Watch Later playlist if opened. This worked good enough.

![Screenshot of main page](https://raw.githubusercontent.com/byronwall/youtube-recs/master/docs/00-main-screen.png)

## News Reader (2020)

This app was a simple RSS reading application. It was built to play with the `newspaper` Python library. It was also a playground to test various Python server techniques since I was about to start something similar at work. The front end was built with the typical React setup.

Features:

- TODO: add this content

Check it out on [Github](https://github.com/byronwall/news-project)

## Task List

Every programmer has to create a task list app! This is mine. There is an incomplete v2 which is a port of the original v1 app. THe original was built with vanilla JS and without React using Electron. The second version was built with Typescript and React. The development experience is much nicer working on v2 with all the modern tooling and frameworks. Part way through v2 I realized there was not much reason to keep using Electron. At that point, I backed off development instead of removing Electron. I may at some point get this finished. Around the time I stopped development, I also changed how I was tracking tasks at work.

Check it out on GitHub: [v1](https://github.com/byronwall/ElectronTasks) or [v2](https://github.com/byronwall/electron-tasks)

TODO: add a screen shot
