---
layout: post
title:  "Prioritising Site Speed Recommendations"
date:   2016-01-18 00:00:00
category: 2016
description: "Sometimes prioritising recommendations is more important than making them."
tags: [web, performance, webperf, recommendations, prioritisation]
comments: true
image:
  feature: "prioritisation_hero.jpg"
---
#### Sometimes prioritising recommendations is more important than making them.

One of my favourite tasks is to provide reports to clients which make recommendations to improve site speed. Often these reports are taken very seriously, senior managers using them to help drive the development road map for the next few months.

The reason for me enjoying these reports so much is because you can often see a direct positive change off the back of them. Like most IT professionals I miss the evolutionary pleasure of working hard to create something with my hands, to have the sense of completion at the end of a project.

Seeing changes based on my recommendations, speed indexes improving and conversion rate increasing, is one of the few 'tactile' pieces of feedback I have on my work.  


Perhaps the most surprising part of delivering these reports is that quite a few of the recommendations I make are already in the backlog. There's invariably at least one 'aha' moment when so.ething truly unknown is discovered, but the vast majority of the improvements are best practises and relatively easy to observe.

The last few of these types of engagements have led me to a realisation. For most of my clients these reports are used as a formal document to *prioritise* site speed improvement work, not just to discover it.  

> There's little value in telling a client about the best practices they've already implemented.

My document structure has evolved due to this. There's little value in telling a client about the best practices they've already implemented, nor is there any point in documenting the fact that they could shave another 10kB off their image weight.

Site speed optimisations can be ranked by two critical factors:

 * what impact it will have on the users
 * how hard it will be to implement

If you can put a rough estimate for these two factors against each recommendation then you can rapidly determine the highest priorities for development. The [MoSCoW](https://en.m.wikipedia.org/wiki/MoSCoW_method) Method gives a good methodology around describing priorities and I often reduce this to a three star system: ★ is could do up to ★★★ for must do. For the ease of implementation, ★ means difficult and ★★★ is simple to change.


I've borrowed from a recent report to demonstrate this theory in practise, below is a small section from the resulting table:

|Recommendation|Impact on Users|Ease of Implementation|
|-------------:|:-------------:|:--------------------:|
|Enable GZip on CSS|★★★|★★★|
|Reduce upstream cookie size|☆★★|☆★★|
|Replace icon fonts with SVG|☆★★|☆☆★|
|Review thrid-party content|☆☆★|☆☆★|
|Remove redundant / unnecessary JavaScript|☆★★|☆☆★|
|Remove redirects|☆☆★|☆★★|

The sum of the stars give a good idea of priority. Take the uncompressed CSS for example: enabling compression should be trivial on any modern set-up, and as CSS is critical to render a page it should be delivered as soon as possible.

> I place the top 5 to 10 highest priority issues in the executive summary, with the full table in the conclusions.

This gives enough up front to give an idea of the issues that have been found, with the addition of the full list for internal prioritisation.
The rest of the report document describes the methodology for determining the recommendations, as well as how each MoSCoW recommendation is made.

For the structure of the recommendations, I usually break it down into four main focus areas:

 * Reduce Requests
 * Reduce Transmitted Bytes
 * Improve Render Performance
 * Review Third-Party Content

In each one I detail what has been discovered, why it is important and how it can be fixed. Perhaps there's another post in that.
