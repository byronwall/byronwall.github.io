---
published: true
title: HTML / CSS / JavaScript Projects
layout: post
category: project
---

This is a rough summary of the various web based projects that I have completed over the years. I have a passion for trying out whatever new technology is out there. Usually a new framework or library makes a previous project much more doable, and it's a good excuse to finish a project and learn something new.

My major web project was the runnDAILY website [which is written up elsewhere](/project/runndaily-portfolio-page/). These other projects focused on other aspects of web development.

## respeller (2019)

This is a simple CLI tool for fixing spelling mistakes in text files. I mainly created it to simplify editing my [Excel VBA book](/projects/excel-vba-book). For better or worse my approach when writing the first draft was to never stop typing. If there was a mistake, I blasted right through it and kept going. This worked great for maintaining a cadence while typing but was awful for editing. I was surprised to find there was not a simple tool to correct mistakes in multiple files. respeller was my solution. Its key feature is the ability to correct a bunch of files at once. It can either find mistakes or correct them. I was OK with it sometimes choosing the wrong word. I figured I would catch bad words when editing but did not want to catch spelling errors.

Check it out on [Github](https://github.com/byronwall/respeller) or [npm](https://www.npmjs.com/package/respeller).

## mathPAD (2010?)

[**Source on GitHub**](https://github.com/byronwall/mathPAD)

**Live version** at [http://byroni.us/mathPAD/](/mathPAD/)

mathPAD is an ongoing project which provides a blank page to perform math and other operations. It was originally destined to be a web based replacement for MathCad. It captured some of the features in MathCad, and I still have plans to extend it further. The most interesting aspect of mathCAD is its ability to parse all of the formulas and math on the page and evaluate the results correctly, including units for engineering calculations. It has a couple of nice features:

- Built in set of standard engineering and science units.
- Units are handled internally as variable definitions so they can be passed around as needed
- Ability to define functions which take parameters. These can also return with or without units.
- Click anywhere and type allows for rapid conversion of numbers and quick testing as a math scratch pad.

I hope in the future to expand mathPAD to allow for:

- Additional units and the ability to save and define unit sets (including possible default outputs)
- Visualization and graphics by integrating with d3 or another framework
- Ability to save and reload previous files. This also prevents some of the benefit of a stateless scratch pad, but it might be nice to save a common file.

Example usage showing unit conversions and variable declaration

![Example](/images/posts/mathpad.png)

## d3 Visualizations

I have been interested in d3 since it was created and I started seeing examples of its output. It's impressive how little code is required to get a rich visualization. In order to get experience with this library, I have used it for a couple of applications:

- Visualization for monitoring variables in a process diagram and coloring/sizing the lines and shapes with the data involved. This is a part of a larger project to provide better data visualization software for process based industries.
- Created a map of all the locations that I visited in the summer of 2014 when I left Houston and moved to Denver. I used d3 to render the map, routes, and cities that we visited. This included shading for states that we visited and drawing the route in the correct order.

I am currently combining d3 with the Electron shell for a data visualization application. [See that project on GitHub](https://github.com/byronwall/data-viz-electron).
