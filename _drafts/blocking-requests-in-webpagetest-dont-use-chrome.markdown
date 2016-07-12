---
title: Blocking requests in webpagetest? Don't use Chrome.
date: 2016-07-11 14:01:00 Z
---

We know that third-party content can harm the user experience on a website. Measuring that impact can be tricky.

In order to demonstrate the performance impact that third-party content can have, I like to remove the offending requests to show a before & after view of a web page. Nothing says 'your third-parties are harming user experience' quite like a video of a page loading twice as fast without them.

To do this, I run a test in webpagetest and get the list of domains as JSON. I parse this to filter out first-parties then re-run the test with all of those domains blocked by webpagetest.

Let's take an example: [cyclingweekly.co.uk](http://www.cyclingweekly.co.uk/). Not for any reason other than I like bikes. When you load the homepage, approximately 150 objects are loaded from 60 domains:
<iframe seamless id="requestmap" style="background-color: transparent;border: 0px none transparent;padding: 0px;overflow: hidden;margin-top:-10px;" src="http://requestmap.webperf.tools/headless.php?id=160712_4N_b3f4e12bc1e1f5058c769a029ff52616" width="100%" height="360px"/>