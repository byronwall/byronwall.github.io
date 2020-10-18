---
layout: post
category: project
published: true
title: React Portfolio
---

I have been using React for the last 4 years for side projects and at work. This page summarizes all of the projects I've built using React. Over the last 4 years, I have progressed significantly in building React apps. My two "flagship" projects were built in the last 2 years working at Allison Transmission. Those include a data analysis platform and an interactive hydraulic schematic tool. Unfortunately, I can only describe those projects and not share sources. Other projects for personal interests include an offline Hacker News reader, a family recipe and cooking site, and an RSS reader for news sites.

My typical setup:

- Use TypeScript exclusively now
- Server typically done with Node.JS
- React Component classes (instead of functional components). I've found these much easier to use with TypeScript. I also don't mind the verbosity.
- Blueprint.js for standard UI/UX Components
- Lodash for standard utility functions
- d3.js for data visualization

## HN Offline (2018 - 2020)

This is a simple web app to read Hacker News comments by storing a local copy. App uses service workers and local storage to provide fully offline HN reading. The goal of this app is to read the comments. It does not provide an offline version of any articles or non-HN links. Server is built with Node.JS and Express.

Features of the site:

- Optimized for lurking. No ability to login, comment, or do anything other than read comments and follow links.
- Three main views for accessing stories: front page, day, and week. Each view provides 50 stories.
- App locally stores HN pages that have been visited to grey them out on the main page.
- Any links to other HN articles are automatically loaded in the app.
- While reading comment threads, an optimized UX is provided to collapse and maintain scrolling.

View it [live](https://hn.byroni.us) or at [Github](https://github.com/byronwall/hn-client)

![HN Offline screenshot](https://raw.githubusercontent.com/byronwall/hn-client/master/mobile.png)

## Platform for Exploratory Multivariate Time Series Analysis (2020)

This data analysis platform facilitates analysis of large multivariate data sets. In particular, it is built to analyze transmission test data. The nature of a transmission is a significant number of related but slightly different events (e.g. every range change). The tool helps to decompose a large data file into related events which can then be analyzed as a unit. The power of the platform is its combined emphasis on: speed, powerful visualization, and sensible "it just works" default settings. Internally the platform is called shift(y) since it was originally used to find and analyze shifts in transmission data.

Core features and front end details:

- Front end built using React and TypeScript; around 30k LOC mostly dedicated to React Components and supporting API calls
- Client/server communication takes place mostly over web sockets; JSON API
- Relies heavily on d3.js and DC.js for graphics and data exploration
  - Extends DC.js with improved controls and performance on its scatter plots
- Built several custom charting components to support frequency analysis (FFTs and spectrograms)
- Automated reporting system which can export compiled charts to PDF
- Novel approaches to exploring and investigating multivariate time series data

To see details related to the C# backend, head over to the [C# Portfolio](/projects/c-sharp).

## Interactive Hydraulic Schematic Tool (2020)

The Interactive Schematic tool was built to provide enhanced features for hydraulic schematics. The existing schematics are PDF files showing the positions of various components for each transmission range/state. Other interactive tools exist but have several downsides related to complex editing processes. In particular, the previous schematics were all built "in code" and required editing and recompiling code to make changes.

Features of the new tool:

- Built using React and TypeScript; deployed via Electron
- Schematic tool is simultaneously an editor and viewer of schematics
- In viewing mode it provide a new advanced features to help hydraulic investigations
- In editing mode it provides a dedicated interface related to creating hydraulic features: valve geometry, tracking, connectivity
- Internal structures maintain a physical model of the hydraulic system
- Schematics are built with different "states" which allow describing the changes between ranges or other failure modes

## Family Recipe and Cooking App (2020)

Simple web app for tracking family recipes. Built using Node.JS and React with TypeScript. App is used regularly by family to simplify our lives in the kitchen. Integrates with the Kroger API to support item searches and adding to a shopping cart. Site was built after my wife could not find a cooking app which had the features she wanted.

Check out on [Github](https://github.com/byronwall/recipe-app).

![Screenshot of meal plan](https://raw.githubusercontent.com/byronwall/recipe-app/master/docs/meal_plan.png)

## YouTube Recommender (2018)

This is a quick server which is used to make better YouTube playlists. It uses a combination of your Watch Later, Watch History, and the YouTube API to provide better playlists.

The goal of this project was to make it easier to select good content from a Watch Later playlist that had more than 500 items. I was using that playlist as a dumping ground for things that might be good. The approach was simple: use the positivity ratio (thumbs up / down) to weight the view count. This gave a nice balance of highly positive content with low view counts and moderately good content that was heavily viewed. When building a playlist it also only allowed a single video per channel at a time. This prevented a single popular channel from dominating.

Overall, it built very nice playlists which could then be picked through more easily.

The client was just a simple interface for creating the playlists. The hardest part of all of this was accessing the watch later playlist. Unfortunately, YouTube does not let you access this playlist for a user (even if authenticated). To get around that, I created a simple bookmarklet which could process the Watch Later playlist if opened. This worked good enough.

Server is built with Node.JS and Express.

Check out on [Github](https://github.com/byronwall/youtube-recs).

![Screenshot of main page](https://raw.githubusercontent.com/byronwall/youtube-recs/master/docs/00-main-screen.png)

## News Reader (2020)

This app was a simple RSS reading application. It was built to play with the `newspaper` Python library. It was also a playground to test various Python server techniques since I was about to start something similar at work. The front end was built with the typical React setup. This site is really a simple RSS reader. When requesting content from an RSS feed, it relays that request through `newspaper` which downloads only the textual content of the article. This mostly works but quality varies by site.

Check it out [live](https://news.byroni.us) or on [Github](https://github.com/byronwall/news-project)

![News list](/images/posts/news-list.png)

![News story](/images/posts/news-story.png)

## Task List (2017 - 2020)

Every programmer has to create a task list app! This is mine. There is an incomplete v2 which is a port of the original v1 app. THe original was built with vanilla JS and without React using Electron. The second version was built with Typescript and React. The development experience is much nicer working on v2 with all the modern tooling and frameworks. Part way through v2 I realized there was not much reason to keep using Electron. At that point, I backed off development instead of removing Electron. I may at some point get this finished. Around the time I stopped development, I also changed how I was tracking tasks at work.

Check it out on GitHub: [v1](https://github.com/byronwall/ElectronTasks) or [v2](https://github.com/byronwall/electron-tasks)

![v1 screenshot](/images/posts/electron-task.png)
