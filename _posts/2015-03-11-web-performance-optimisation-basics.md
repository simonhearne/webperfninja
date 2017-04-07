---
title: Web Performance Optimisation Basics
date: 2015-03-11 19:54:00 Z
categories:
- '2015'
tags:
- web performance
- webperf
- rules
layout: post
comments: true
image:
  feature: speed_hero.jpg
excerpt: Website performance is critical to user experience. We need rules to make it easier.
---


Our web performance industry was unquestionably seeded by Steve Souders' book [High Performance Websites](http://shop.oreilly.com/product/9780596529307.do). In his book, steve identifies [14 rules](http://stevesouders.com/hpws/rules.php) to improve web perfomance.

As part of my job at NCC Group I get to produce optimisation reports for our customers (called healthchecks). In these reports we tend to focus on five key areas, one of these is front-end optimisation. This is where Steve's rules come in. The rules were first published in 2007, over 8 years ago! In the fast-paced world of technology this is a huge amount of time, although admittedly the technology that defines the web has not changed too much since then. Web browsers and business attitudes to web performance have changed, however. Companies are focusing more effort and resource on ensuring a good online experience for their customers. Gradually, web performance is being considered as one of the key factors in the customer experience.

What we need now is a concise, logical list of technical recommendations to improve website performance.

The list needs to be logical in terms of implementation and importance, but must also have business context in terms of complexity of implementation. Generally, improving front-end performance reduces operational cost: fewer bytes over a CDN is less $ spent, fewer connections to a firewall is less utilisation. There is also an associated cost - implementing combined CSS involves process changes, new technologies etc.

The challenge is finding a generic enough list of recommendations which will apply across website industries, customer types, mobile v. desktop etc. I have tried to create a list which covers these elements but only caters for browser activity before the onLoad event (according to [wikipedia](http://en.wikipedia.org/wiki/DOM_events) the onLoad event "fires when the [user agent](http://en.wikipedia.org/wiki/User_agent "User agent") finishes loading all content within a document, including window, frames, objects and images"). Content requested after onLoad _should not_ impact customer experience - this is the realm for analytics, tracking, advertising etc. Here's my current working draft of pre-onLoad recommendations:

*   Make fewer requests
    *   Combine CSS
    *   Combine JS
    *   Sprite small images
    *   Cache everything (no ETags?)
*   Transmit fewer bytes
    *   Optimise Images
    *   Compress everything
    *   Send only what you need (responsive images?)
    *   Cache everything
*   Reduce request latency
    *   Optimise the application
    *   Use asynchronous requests
    *   Put content close to the consumer
    *   Optimise headers
    *   Use the latest protocols
    *   Set an intelligent initial congestion window
*   Prioritise critical content
    *   Inline critical CSS
    *   Inline critical images
    *   Inline critical JS
    *   Outline non-critical content
    *   Load images asynchronously
*   Remove single points of failure
    *   Use async & defer
    *   Manage third-parties (tag management?)
    *   Re-consider <link src> tags

The specific implementation of each recommendation is unimportant, but the general concepts and prioritisation are key to getting a website to perform at its best.

Feedback graciously welcomed!

Si.
