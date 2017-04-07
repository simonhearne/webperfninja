---
title: Using a Web Performance Heatmap to Assess Page Performance
date: 2015-05-29 15:30:00 Z
categories:
- '2015'
tags:
- web performance webperf heatmap
layout: post
image:
  feature: heatmap_hero.jpg
excerpt: I've made a [Web Performance Heatmap](http://heatmap.webperf.tools/ "Web
  Performance Heatmap") to visualise when each element loads on a page.
---

<a href="http://heatmap.webperf.tools" class="btn btn-block btn-primary">Go to the tool</a>

I've recently had a few clients ask if there is a way to test when certain parts of their pages become visually complete. Imagine a media company that relies on advertising revenue who wants to measure when the above-the-fold adverts are rendered, relative to the actual content of the page.   

We have a few ways to attempt this, for example [user timings](http://www.html5rocks.com/en/tutorials/webperformance/usertiming/ "HTML5Rocks User Timings Tutorial") can add a performance timing marker based on an element loading (note that this can't tell when the loaded element / image is actually rendered). To really tell when an element is rendered we either need to dig in to [paint traces](https://www.chromium.org/developers/how-tos/trace-event-profiling-tool/trace-event-reading "Chromium about:tracing page") or use a filmstrip view from e.g. [webpagetest](http://webpagetest.org "WebPageTest.org").   

The only realistic solution to tell when an element on a page _actually_ renders in a controlled environment is to use a filmstrip view and scroll through until the relevent part of the page is visible. This is obviously a labour-intensive task and tricky to automate.   

Thinking about better solutions to this challenge led me to imagine a heatmap of a webpage - showing in red-amber-green how late each pixel was to load. This would make it simple to tell, at a glance, what parts of the page are slow or fast to render.   

To test this theory out I started running filmstrips from WebPageTest through PHP to compare pixels to the final frame and determine when each pixel achieved its final state. Doing this I discovered that by default WebPageTest filmstrip images are scaled and heavily compressed. While to remove the scaling you have to re-build the WebPageTest agent, you can disable image compression [using a hidden form field](http://jrvis.com/blog/wpt-screenshots/). Now that I had uncompressed images I could write a function that iterates through the frames and notes at what load time each pixel completes. This matrix can then be used to generate a heatmap layer based on the performance budget (e.g. if a pixel acheives final state at 8 seconds and the budget is 6 seconds, colour the pixel red).   

I ended up building a wrapper on top of WebPageTest to automate this process and generate a heatmap for you: [heatmap.webperf.tools](http://heatmap.webperf.tools/ "Web Performance Heatmap").   

<figure>
<a href="http://heatmap.webperf.tools/render/150527_SH_827d2295b66e4180892db766eaf8a492/10000" target="_blank">
<img src="/images/heatmap_pinterest.png"/>
<figcaption>Pinterest Heatmap highlighting that the top images are late to load (click to interact).</figcaption></a>
</figure>

So go ahead - have a play. Note that it is a proof-of-concept toy not a complete tool so please let me know what you think.   

_You may notice some strange results when you test your website. Many websites have rotating carousels or cookie / advert banners which push all of the page content down, this causes the heatmap to reflect potentially poor results even though content has been rendered earlier. My opinion on this is that shifting the page down for a cookie / advert banner is bad for user experience. [So is using a rotating carousel](http://shouldiuseacarousel.com/ "Should I Use a Carousel?")._