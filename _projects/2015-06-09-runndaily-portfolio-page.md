---
published: true
title: runnDAILY portfolio page
layout: post
category: blog
---


## runnDAILY
runnDAILY was a website that I created with Chandler Wall back when we were at Purdue.  At the time we were both fairly serious runners (and might still claim to be) and were underwhelmed with the fitness tracking websites.  This was circa 2009 when the iPhone was new and my Windows Phone had a slide out keyboard (and stylus in the antenna).  We recognized a need for an outdoor fitness tracker that we actually wanted to use.  At the time Map My Run was the only serious web site trying this.

The site was up and running for 3 years and saw 2 major updates over that time.  Interest in developing the site languished once we both got full time jobs and did not need to "make it" in order to be something after Purdue.  It was good work to have a real site out on the internet.  When we closed things down at the end, there were 8 active users.  Sorry guys!

The site was built on a LAMP stack although we developed on Windows.  It's core features were a combination of standard server side DB CRUD and a good client side of features including Google Maps integration.

The server side include included:

 - PHP based pages that almost used an MVC framework for managing data and display
 - I built a templating system that used Smarty style tags to process the data into HTML or JSON data.  This templating engine was fairly powerful and had the feature that all the cascading levels were parsed into a single executable PHP file that was included after the page routing code ran.  This kept things fast and reduced server side file loading all the time.
 - MySQL database with no frills.  We used a large number of many to many table relationships to manage the site permissions and user relationships.
 - Subversion for version control which made deploying updates nice.

Client side featured:

 - Heavy AJAX usage to load map or route data
 - A number of Google Map based features that allowed for routing, distance markers, loading nearby routes, and several advanced route creation features.
