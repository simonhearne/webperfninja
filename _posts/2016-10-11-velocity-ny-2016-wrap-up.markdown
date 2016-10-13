---
title: Velocity NY 2016 - Wrap-up
date: 2016-10-11 14:29:00 Z
comments: true
image:
  feature: "../uploads/newyork_hero.jpg"
layout: post
---

Velocity New York seems like a distant memory now, especially with Velocity Europe around the corner. With that said, I have copious notes from the two day conference which I have summarised here. There were a lot of nuggets of wisdom which I’ll try to organise into a logical order.

{:toc}

## Real User Monitoring is getting exciting, but has gaps

Everyone is using RUM. The vendors are maturing rapidly to be able to offer either:

* Single view of customer - integration with Application Performance Monitoring.
* Insight - analysis of user behaviour and business events to create actionable insight.

An example of a vendor going down the second route is SOASTA’s mPulse; there was a lot of discussion around [machine learning](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51082), with conclusions that the highest predictor of bounce rate is DOM Ready time, number of <script>s and DOM elements inversely correlated with conversion rate.

![domnode_conversion.png](/uploads/domnode_conversion.png)

SOASTA also introduced [measuring continuity](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50522), using cool new script snippets to measure user behaviour. For example: measuring dead clicks, frame rate, time between intent and action. It’s all exciting stuff but I have concerns about the impact on user experience that these measurements will have (see [observer effect & bias](http://www.dnb.com/perspectives/data-management-and-analytics/recognizing-observer-effect-issues-in-data-science.html)!). Their experiments are available in a public [GitHub repo](https://github.com/soasta/measuring-continuity).

There is clearly a lot of potential in using RUM to make predictions and measure outcomes. What we’re still missing is tight integration with experiment technology (e.g. Maxymiser or Google Experiments). Without that, we can’t use RUM to properly manage development decisions. [Stuart McMillan](https://twitter.com/mcmillanstu) from Schuh recently mentioned that they use Google Analytics for performance data during experiments, probably because the integration works well. Unfortunately, the site speed data from Analytics is pretty poor… In the example below site speed metrics were only collected for under 1% of pageviews!

![sitespeed_sample.png](/uploads/sitespeed_sample.png)

## Synthetic Monitoring vendors are disappearing from Velocity

There was virtually no presence from synthetic monitoring vendors at Velocity NY, the exception being [Mehdi](https://twitter.com/mdaoudi) from [Catchpoint](http://www.catchpoint.com/). This is a trend that I’ve noticed over the past three years, probably driven by the commoditised synthetic monitoring being bundled into APM solutions (e.g. New Relic’s [Synthetics](https://newrelic.com/synthetics)).

I think this says a lot about the advancement of RUM and APM. Synthetic gives the heartbeat monitoring and alerting for operational awareness, but if you know that your infrastructure and applications are ok, and that customers are having a good experience, then you don’t need synthetic monitoring to tell you a page is available.

## WebPageTest is bigger than ever

Almost every talk referenced [WebPageTest](http://www.webpagetest.org/) or [HTTPArchive](http://httparchive.org/) (which uses WebPageTest under the hood). It has certainly become the defacto web performance testing tool, with companies forming off the back of it such as [SpeedCurve](https://speedcurve.com/). What seems to be missing is contribution back in to the project. Looking at the contributors page on GitHub shows that [Pat](https://twitter.com/patmeenan) is responsible for almost all development on the project. 

Perhaps the industry (including myself) is taking this for granted.

![webpagetest_contributors.PNG](/uploads/webpagetest_contributors.PNG)

## Big companies are talking about site speed

Ancestry and GoDaddy both spoke at Velocity. [Jed Wood](https://twitter.com/silentrant)’s talk about [creating a performance culture](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51033) at Ancestry was insightful, describing the journey from quick wins (gzip, images etc.) to a full understanding of performance. To do this, Ancestry track business metrics such as conversions, alongside user-centric performance metrics such as time to an ancestor’s name rendering. The focus on both business metrics and user-centric metrics means that Jed can demonstrate a correlation to the business to help drive further work on site speed.

Improving the Ancestry.com sign up page from 2.7 seconds to 1.7 generated a 7% increase in conversions. Interestingly, further work to get to 1.3 seconds made no further improvement to conversion. The chart below is taken from SpeedCurve and shows the team's progress over time to reduce Speed Index. What I really like about this is the use of annotations to mark where changes and releases occurred, so changes in performance can be traced back to a specific build of the website.

![ancestry_speedindex.PNG](/uploads/ancestry_speedindex.PNG)

One of the ways Ancestry maintains performance is by adding an artificial delay to third-party scripts executing. I wonder if [requestIdleCallback](https://developers.google.com/web/updates/2015/08/using-requestidlecallback) could be used for this?

[Jim Pierson](https://twitter.com/perfmangodaddy) from GoDaddy took a different approach. To prove that performance was important, he and an engineer [secretly improved the performance](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50588) of the GoDaddy homepage in India, while there was no change in marketing activity. The result of improving load time by 50% was an additional $35,000 of revenue per day. Now if that doesn’t sell the value of performance I’m not sure what will. Those performance tweaks are now rolled out across all of GoDaddy.

Jim used a maturity model to describe his journey in web performance, with anomaly detection, regression analysis and communication being at the top. I think the most important point that Jim made was the need for solid understanding of performance impact across the business. There's nothing quite like $35,000 to do that, I suppose.

![godaddy_maturity.PNG](/uploads/godaddy_maturity.PNG)

## Single Page Apps are slow

I was really happy that someone else said this out loud. [Boris](https://twitter.com/livshitz98) and [Manuel](https://twitter.com/MD_A13) from Akamai talked about [making SPAs faster](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51232) through selecting the right SPA framework, using JS bundlers, server-side rendering and tricking the user with a skeleton page. All of these are hacks around the fundamental problem with client-side applications. As such, I’m not a fan!

I also spoke a lot about SPAs being slow [in my presentation](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51254). In my study, a SPA will generally be 43% slower than a traditional web page. Of course this difference is magnified on mobile devices.


## AMP is not the killer feature

The [Accelerated Mobile Pages](https://www.ampproject.org/) project is over a year old now. There were two talks about AMP which took very different approaches. [Malte Ubl](https://plus.google.com/\+MalteUbl) (creator of AMP) [gave a talk](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50798) about the current state of AMP and what’s coming in the future, while [Nic](https://twitter.com/nicj) and [Nigel](https://twitter.com/querymetrics) of SOASTA used analytics data gathered by mPulse to [describe what consumers were doing with AMP pages](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51319).

One of the interesting points brought up by Malte was that as AMP pages are almost always (>99%) served by the AMP CDN, there is a lot of potential for static performance optimisation. For example, the average image on the AMP CDN can be further compressed to reduce the file size by 40%. Rolling out these optimisations at the CDN level will have a great bang-for-buck across all AMP pages.

Analytics gathered by SOASTA paint a rather gloomy picture for publishers using AMP. While AMP pages are almost six times faster than the regular page, they take users out of the publishers’ domain. The probability of a reader of an AMP article going to the *article publishers’ own site* in the next 30 days is only 3%. So it seems there is a significant trade-off to be had: in order to have super-fast articles that are *promoted by Google in search results*, you have to sacrifice engagement and brand awareness.

This all feels very walled-garden, especially as AMP pages are just optimised web pages, which anyone can make. I like the fact that it promotes fast content as better content, but I don’t think it’s in the publisher’s best interest. [Tim Kadlec](https://twitter.com/tkadlec) has proposed an open alternative to AMP, the [Content Performance Policy](https://timkadlec.com/2016/02/a-standardized-alternative-to-amp/), which is definitely worth read.

## There are lots of underutilised performance and security features on the web

[Sonia](https://twitter.com/soniaburney) and [Sabrina](https://twitter.com/sabrina_burney) Burney of Akamai promised a talk on the [cross-overs in web security and web performance](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51203). The talk was fast-paced and covered a lot of ground including how features we use already (iframes, pre-load etc.) have additional security options that few people use. This was the most practical session of the conference for me, and I need to list all of these out to make sense of it:

### iFrames

Iframes are great for performance, kinda.
Over 60% of sites use iframes, yet virtually none of them use the [sandbox attribute](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/). Sandbox allows you to define what access the iframe has to the parent page and whether it can execute scripts. It will also deny pointer lock, form submissions and a whole host of other scary stuff.

### Prefetch / Preload `As`

Prefetch allows web developers to provide hints to browsers about assets which should be optimistically downloaded. This is great for objects which are critical to render, such as CSS and WebFonts. Prefetch can be used in <link> tags or in HTTP headers, the advantage of a header being that it can be used by the browser before the HTML document has been downloaded and parsed.

Preload builds on prefetch by forcing the browser to download the asset, whereas prefetch hints can be ignored.

Both of these have an additional optional attribute: `as`. This allows us to define the type of asset to be loaded, e.g. 'image', 'script' or any one of the [standard fetch types](https://fetch.spec.whatwg.org/#concept-request-destination). Adding the type of asset allows the browser to send the correct Accept header, as well as ensuring that any content security policy can be applied correctly to the preloaded asset. 

![preload_prefetch-9863b9.png](/uploads/preload_prefetch-9863b9.png)

### Content Security Policy

Speaking of content security policy... This is the header directive which tells a browser what permissions each domain used on a site has. For example, fonts.example.com should not be able to execute scritps, and static.example.com might only be for serving images. Using a [content security policy](https://developers.google.com/web/fundamentals/security/csp/) ensures that only the correct domains have access to the browser, which is obviously a security win. The performance benefit comes mainly from the audit and analysis required in order to write a CSP - what domains are being used on our site, for what, and why?!

### Service Worker

Now we come to service worker, the magic JavaScript proxy thread. This is the concept most fundamental to 'offline-first': a developer-controlled proxy which can intercept network requests, build an internal cache and do all sorts of other magic.

For performance, service worker is critical for good performance in poor network conditions, if you haven't seen [Jake Archibald](https://twitter.com/jaffathecake) talk about service worker yet, check out his [video from Google IO](https://www.youtube.com/watch?v=cmGr0RszHc8). No, seriously, go watch that video.

Now on to security. As service worker has access to network requests, it can be used to enforce rules in a similar way to content security policy. You can even maintain your own black- and white-lists of blocked assets or domains, and let the service worker manage how these are enforced in the browser. Cool, eh?

I think the next logical step is for service workers to apply time thresholds to third-party downloads. That tracker tag taking over a second to load? Kill the request, give a safe response to the browser, and log the event to keep track of how often it happens. The possibilities are almost endless!

### Sub-Resource Integrity

Sabrina and Sonia only briefly mentioned SRI but I think it's worth covering in a little more detail here. SRI allows you to take a hash of an asset (e.g. jQuery v1.9.1, minified) and add that to your ```<script>``` tag. If the downlaoded asset does not have the same hash, then the browser will refuse to execute it. This is really handy for third-party content that has the potential to effect user experience and/or security, or whose provenance is not entirely clear (JavaScript CDNs, anyone?)

```
<script src="https://example.com/example-framework.js"
        integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho1wx4JwY8wC"
        crossorigin="anonymous"></script>
```

![sri.png](/uploads/sri.png) 

## Progressive web apps aren’t all that. Yet.

There was a lot of conversation around [progressive web applications](https://developers.google.com/web/progressive-web-apps/), but the lack of good browser support for some of the key features means that large organisations are holding off implementation: Web Push is only [available on Firefox and Chrome](http://caniuse.com/#feat=push-api), service worker is only [partially supported on Firefox, Chrome and Opera](http://caniuse.com/#feat=serviceworkers).
I'm also wary of websites going fully PWA - which may not provide the desktop with a good experience. Definitely a 'watch this space'.

 



In summary, an awesome conference with huge amounts to mull over.