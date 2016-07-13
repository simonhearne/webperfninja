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

TL;DR: Blocking third-party requests in webpagetest shows you the impact they're having on a page, but Chrome is inefficient at blocking the requests. So use another browser such as Internet Explorer to do third-party impact testing.

In order to demonstrate the performance impact that third-party content can have, I like to remove the offending requests to show a before & after view of a web page. Nothing says 'your third-parties are harming user experience' quite like a video of a page loading twice as fast without them.

To do this, I run a test in webpagetest and get the list of domains as JSON. I parse this to filter out first- & second-party domains then re-run the test with all of the third-party domains blocked by webpagetest. Often, though, just blocking tag container(s) will do the job.

Let's take an example: [cyclingweekly.co.uk](http://www.cyclingweekly.co.uk/). Not for any reason other than I like bikes. When you load the homepage, approximately 150 objects are loaded from 60 domains:

<figure align="center">
<a href="http://requestmap.webperf.tools/render/160712_4N_b3f4e12bc1e1f5058c769a029ff52616">
<img style="max-width:80%;" src="/uploads/cyclingweekly_requestmap.png"/>
</a>
<figcaption>Requestmap of cyclingweekly.co.uk (click to interact)</figcaption>
</figure>

Now to test the impact of this large number of third-parties lets block them and re-run the test. Here's the result:
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_chrome_blocked.jpg"/>
<figcaption>Filmstrip comparison without & with third-party content</figcaption>
</figure>

Kind of what I expected, the third-parties mean the page takes longer to finish. But I had secretly hoped that they were also affecting render performance - that the blocked version would render quicker.

To dig in a bit deeper I looked at the waterfall chart of the blocked version, and I noticed two things: the requests seemed to be sequential rather than parallel, and the CPU was pegged at 100% for most of the time. Curious.
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_waterfall.png"/>
<figcaption>Waterfall chart showing sequential requests when third-parties are blocked</figcaption>
</figure>

Whenever the CPU is pegged in a Chrome webpagetest result, here's a pro-tip: enable timeline capture. 
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_devtoolscapture.png"/>
<figcaption>Enabling timeline capture in webpagetest</figcaption>
</figure>

This gives you a json file that you can drag into your local Chrome developer tools window:
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_timelinelink.png"/>
<figcaption>Download timeline json</figcaption>
</figure>

Loading this up in Chrome Canary lets you analyse the network waterfall in the timeline view, where I saw significant gaps in the processing timeline, and a number of grey requests:
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_timeline_gaps.png"/>
<figcaption>Blocked requests appearing and gaps in timeline</figcaption>
</figure>

The grey request was one which should have been blocked by webpagetest. You can't drill into any more details from this view, although it looks like the blocked requests still consume time yet don't have a response.

In [issue 584](https://github.com/WPO-Foundation/webpagetest/issues/584) on the webpagetest GitHub repo Pat Meenan states:
> blocking (or modifying request headers) in Chrome is exceedingly expensive

So, trying again in Firefox and Internet Explorer we get the following results:
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_allwaterfalls.png"/>
<figcaption>Waterfall charts for three browsers while blocking third-party domains</figcaption>
</figure>

And for visual performance, IE gives the best result:
<figure align="center">
<img style="max-width:80%;" src="/uploads/cyclingweekly_allfilmstrips.png"/>
<figcaption>Waterfall charts for three browsers while blocking third-party domains</figcaption>
</figure>

So the final result, to show the impact of third-party content on the user experience comes out below:
<figure align="center">
<a href="http://www.webpagetest.org/video/compare.php?tests=160713_R1_c806002ca46eb2f775660192cc9086bd,160713_EM_6602f7fa269476d6430c84d5e30f6f24">
<img style="max-width:95%;" src="/uploads/cyclingweekly_ieblocked2.png"/>
</a>
<figcaption>Filmstrip image showing with cyclingweekly.co.uk loading without & with third-party assets (click to see in webpagetest)</figcaption>
</figure>