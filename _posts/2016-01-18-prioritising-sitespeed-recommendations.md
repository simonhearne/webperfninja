---
title: Prioritising Site Speed Recommendations
date: 2016-01-18 00:00:00 Z
categories:
- '2016'
tags:
- web
- performance
- webperf
- recommendations
- prioritisation
layout: post
description: Sometimes prioritising recommendations is more important than making
  them.
comments: true
image:
  feature: prioritisation_hero.jpg
---

#### Sometimes prioritising recommendations is more important than making them.

One of my favourite tasks as a consultant is to provide reports to clients which make recommendations for improving site speed. Often these reports are taken very seriously, with senior managers using them to help drive the development roadmap for the next few months.

The reason I enjoy these reports so much is that you can often see a direct positive change off the back of them. Like most IT professionals I miss the intrinsic pleasure of working hard to create something with my hands, to have the [sense of completion](http://changingminds.org/explanations/needs/completion.htm) at the end of a project.

Seeing changes based on my recommendations, speed indexes improving and conversion rate increasing, is one of the few 'tactile' pieces of feedback I have on my work.  

> The vast majority of the improvements are best practises and relatively easy to observe

Perhaps the most surprising part of delivering these reports is that quite a few of the recommendations I make are already in the client's backlog. Luckily there is invariably at least one 'aha' moment when something truly unknown is discovered, but the vast majority of the improvements are best practises and relatively easy to observe.

The last few of these types of engagements have led me to a realisation; for most of my clients these reports are used as a formal document to *prioritise* site speed improvement work, not just to discover it.  

> There's little value in telling a client about the best practices they've already implemented.

My document structure has evolved due to this. There's little value in telling a client about the best practices they've already implemented, nor is there any point in documenting the fact that they could shave another 10kB off their image weight.

So in my reports I now suggest that site speed optimisations can be ranked by two critical factors:

 * what impact will this change have on the users
 * how hard will the change be to implement

If you can put a rough estimate for these two factors against each recommendation then you can rapidly determine the highest priorities for development. The [MoSCoW](https://en.m.wikipedia.org/wiki/MoSCoW_method) Method gives a good methodology around describing priorities and I often reduce this to a three star system: ★ is could do up to ★★★ for must do. For the ease of implementation ranking: ★ means difficult and ★★★ is simple to change.


I've borrowed from a recent report to demonstrate this theory in practise, below is a small section taken from the results table:

|Recommendation|Impact on Users|Ease of Implementation|
|-------------:|:-------------:|:--------------------:|
|Enable gzip on CSS|★★★|★★★|
|Reduce upstream cookie size|☆★★|☆★★|
|Replace icon fonts with SVG|☆★★|☆☆★|
|Review third-party content|☆☆★|☆☆★|
|Remove redundant JavaScript|☆★★|☆☆★|
|Remove redirects|☆☆★|☆★★|

The sum of the stars give a good idea of priority. Take the uncompressed CSS issue for example: enabling gzip compression should be trivial on any modern set-up, and as CSS is critical to render a page it should be delivered as soon as possible.

> I place the highest priority issues in the executive summary, with the full table in the conclusion.

This gives enough up front to give an idea of the issues that have been found, with the addition of the full list for internal prioritisation.
The rest of the report describes the methodology for making the recommendations, as well as how each MoSCoW recommendation is made.

For the structure of the recommendations, I usually break it down into four of these main focus areas:

 * Reduce Requests
 * Reduce Transmitted Bytes
 * Improve Render Performance
 * Review Third-Party Content
 * Improve Back-end Performance

In each one I detail what has been discovered, why it is important and how it can be fixed. Perhaps there's another post in that.
