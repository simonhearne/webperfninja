---
title: Blocking requests in webpagetest? Don't use Chrome.
date: 2016-07-11 14:01:00 Z
categories:
- '2016'
tags:
- webpagetest
layout: post
---

We know that third-party content can harm the user experience on a website. Measuring that impact can be tricky.

In order to demonstrate the performance impact that third-party content can have, I like to remove the offending requests to show a before & after view of a web page. Nothing says 'your third-parties are harming user experience' quite like a video of a page loading twice as fast without them.

To do this, I run a test in webpagetest and get the list of domains as JSON. I parse this to filter out first-parties then re-run the test with all of those domains blocked by webpagetest. Often, though, just blocking tag container(s) will do the job.

Let's take an example: [cyclingweekly.co.uk](http://www.cyclingweekly.co.uk/). Not for any reason other than I like bikes. When you load the homepage, approximately 150 objects are loaded from 60 domains:
<iframe seamless id="requestmap" style="background-color: transparent;border: 0px none transparent;padding: 0px;overflow: hidden;margin-top:-10px;" src="http://requestmap.webperf.tools/headless.php?id=160712_4N_b3f4e12bc1e1f5058c769a029ff52616" width="100%" height="360px"/>

Now to test the impact of this large number of third-parties lets block them and re-run the test. Here's the result:
![cyclingweekly_chrome_blocked.png](/uploads/cyclingweekly_chrome_blocked.png)

Kind of what I expected, the third-parties mean the page takes longer to finish. But I had secretly hoped that they were also affecting render performance - that the blocked version would render quicker.

To dig in a bit deeper I looked at the waterfall chart of the blocked version, and I noticed two things: the requests seemed to be sequential rather than parallel, and the CPU was pegged at 100% for most of the time. Curious.
![cyclingweekly_waterfall.png](/uploads/cyclingweekly_waterfall.png)

Whenever the CPU is pegged in a Chrome webpagetest result, here's a pro-tip: enable timeline capture. 
![cyclingweekly_devtoolscapture.png](/uploads/cyclingweekly_devtoolscapture.png)

This gives you a json file that you can drag into your local Chrome developer tools window:
![cyclingweekly_timelinelink.png](/uploads/cyclingweekly_timelinelink.png)

Loading this up in Chrome Canary lets you analyse the network waterfall in the timeline view, where I saw significant gaps in the processing timeline, and a strange grey request:
![cyclingweekly_timeline_gaps.png](/uploads/cyclingweekly_timeline_gaps.png)

The grey request was one which should have been blocked by webpagetest. It returned an empty 200 response
