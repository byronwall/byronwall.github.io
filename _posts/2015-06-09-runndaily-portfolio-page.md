---
published: true
title: runnDAILY
layout: post
category: project
---

runnDAILY was a website that mapped and traced outdoor fitness activities.  I created it with Chandler Wall back when we were at Purdue.  At the time we were both fairly serious runners (and might still claim to be) and were underwhelmed with the fitness tracking websites.  This was circa 2009 when the iPhone was new and my Windows Phone had a slide out keyboard.  We recognized a need for an outdoor fitness tracker that we actually wanted to use.  At the time MapMyRun was the only serious web site trying this.

The site was up and running for 3 years and saw 2 major updates over that time.  Interest in developing the site languished once we both got full time jobs, but we did push one major update after we graduated.  It was rewarding to have a real site out on the internet.

## Images of design and features

**Main index page**

![runnDAILY main page](/images/posts/runnDAILY/index.png)

**Route creation page**

![runnDAILY route creation page](/images/posts/runnDAILY/routes.png)

## Features

[**Source on GitHub**](https://github.com/byronwall/runnDAILY)

The site was built on a LAMP stack although we developed on Windows.  It's core features were a combination of standard server side DB CRUD and client side interactivity via JavaScript, including Google Maps integration.

The server side include included:

 - PHP based pages that almost used an MVC framework for managing data and display
 - I built a templating system that used Smarty style tags to process the data into HTML or JSON data.  This templating engine was fairly powerful and had the feature that all the cascading levels were parsed into a single executable PHP file that was included after the page routing code ran.  This kept things fast and reduced server side file loading all the time.
 - MySQL database with no frills.  We used a large number of many to many table relationships to manage the site permissions and user relationships.
 - Subversion for version control which made deploying updates nice.

Client side featured:

 - Heavy AJAX usage to load map and route data
 - A number of Google Map based features that allowed for routing, distance markers, loading nearby routes, and several advanced route creation features.
