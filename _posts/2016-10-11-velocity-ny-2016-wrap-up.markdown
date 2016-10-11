---
title: Velocity NY 2016 - Wrap-up
date: 2016-10-11 14:29:00 Z
layout: post
---

Velocity New York seems like a distant memory now, especially with Velocity Europe around the corner. With that said, I have copious notes from the two day conference which I will try to summarise here. There were a lot of nuggets of wisdom which I’ll try to organise into a logical order.

{:toc}
## Real User Monitoring is getting exciting, but has gaps

Everyone is using RUM. The vendors are maturing rapidly to be able to offer either:
 * Single view of customer - integration with Application Performance Monitoring.
 * Insight - analysis of user behaviour and business events to create actionable insight.

An example of a vendor going down the second route is SOASTA’s mPulse; there was a lot of discussion around [machine learning](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51082), with conclusions that the highest predictor of bounce rate is DOM Ready time, number of <script>s and DOM elements inversely correlated with conversion rate. SOASTA also introduced [measuring continuity](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50522), using cool new script snippets to measure user behaviour. For example, measuring dead clicks, frame rate, time between intent and action. It’s all exciting stuff but I have concerns about the impact on user experience that these measurements will have (see [Observer Effect & Bias](http://www.dnb.com/perspectives/data-management-and-analytics/recognizing-observer-effect-issues-in-data-science.html)!).

There is clearly a lot of potential in using RUM to make predictions and measure outcomes. What we’re still missing is tight integration with experiment technology (e.g. Maxymiser or Google Experiments). Without that, we can’t use RUM to properly manage development decisions. [Stuart McMillan](https://twitter.com/mcmillanstu) from Schuh recently mentioned that they use Google Analytics for performance data during experiments, probably because the integration works well. Unfortunately, the site speed data from Analytics is pretty poor…

## Synthetic Monitoring vendors are disappearing from Velocity

There was virtually no presence from synthetic monitoring vendors at Velocity NY, the exception being [Mehdi](https://twitter.com/mdaoudi) from [Catchpoint](http://www.catchpoint.com/). This is a trend that I’ve noticed over the past three years, probably driven by the commoditised synthetic monitoring being bundled into APM solutions (e.g. New Relic’s [Synthetics](https://newrelic.com/synthetics)).

I think this says a lot about the advancement of RUM and APM. Synthetic gives the heartbeat monitoring and alerting for operational awareness, but if you know that your infrastructure and applications are ok, and that customers are having a good experience, then you don’t need synthetic monitoring right then.

## WebPageTest is bigger than ever

## Big companies are talking about site speed
Ancestry and GoDaddy both spoke at Velocity. [Jed Wood](https://twitter.com/silentrant)’s talk about [creating a performance culture](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51033) at Ancestry was insightful, describing the journey from quick wins (gzip, images etc.) to a full understanding of performance. To do this, Ancestry track business metrics such as conversions, alongside user-centric performance metrics such as time to an ancestor’s name rendering. The focus on both business metrics and user-centric metrics means that Jed can demonstrate a correlation to the business to help drive further work on site speed.

Improving the Ancestry.com sign up page from 2.7 seconds to 1.7 generated a 7% increase in conversions. Interestingly, further work to get to 1.3 seconds made no further improvement to conversion.

One of the ways Ancestry maintains performance is by adding an artificial delay to third-party scripts executing. I wonder if [requestIdleCallback](https://developers.google.com/web/updates/2015/08/using-requestidlecallback) could be used for this?

[Jim Pierson](https://twitter.com/perfmangodaddy) from GoDaddy took a different approach. To prove that performance was important, he and an engineer [secretly improved the performance](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50588) of the GoDaddy homepage in India, while there was no change in marketing activity. The result of improving load time by 50% was an additional $35,000 of revenue per day. Now if that doesn’t sell the value of performance I’m not sure what will. Those performance tweaks are now rolled out across all of GoDaddy.

Jim used a maturity model to describe his journey in web performance, with anomaly detection, regression analysis and communication being at the top.
[insert image here]

## Single Page Apps are slow
I was really happy that someone else said this out loud. [Boris](https://twitter.com/livshitz98) and [Manuel](https://twitter.com/MD_A13) talked about [making SPAs faster](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51232) through selecting the right SPA framework, using JS bundlers, server-side rendering and tricking the user with a skeleton page. All of these are hacks around the fundamental problem with client-side applications. As such, I’m not a fan!

I also spoke a lot about SPAs being slow [in my presentation](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51254). In my study, a SPA will be 43% slower than a traditional web page. Of course this difference is magnified on mobile devices.
[insert image from my talk here]
## AMP is not the killer feature
The [Accelerated Mobile Pages](https://www.ampproject.org/) project is over a year old now. There were two talks about AMP which took very different approaches. [Malte Ubl](https://plus.google.com/+MalteUbl) (creator of AMP) [gave a talk](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/50798) about the current state of AMP and what’s coming in the future, while [Nic](https://twitter.com/nicj) and [Nigel](https://twitter.com/querymetrics) of SOASTA used analytics data gathered by mPulse to [describe what consumers were doing with AMP pages](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51319).

One of the interesting points brought up by Malte was that as AMP pages are almost always (>99%) served by the AMP CDN, there is a lot of potential for static performance optimisation. For example, the average image on the AMP CDN can be further compressed to reduce the file size by 40%. Rolling out these optimisations at the CDN level will have a great bang-for-buck across all AMP pages.

Analytics gathered by SOASTA paint a rather gloomy picture for publishers using AMP. While AMP pages are almost six times faster than the regular page, they take users out of the publishers’ domain. The probability of a reader of an AMP article going to the *article publishers’ own site* in the next 30 days is only 3%. So it seems there is a significant trade-off to be had: in order to have super-fast articles that are *promoted by Google in search results*, you have to sacrifice engagement and brand awareness.

This all feels very walled-garden, especially as AMP pages are just optimised web pages, which anyone can make. I like the fact that it promotes fast content as better content, but I don’t think it’s in the publisher’s best interest.

## There are lots of underutilised performance and security features on the web

[Sonia](https://twitter.com/soniaburney) and [Sabrina](https://twitter.com/sabrina_burney) Burney of Akamai promised a talk on the [cross-overs in web security and web performance](http://conferences.oreilly.com/velocity/devops-web-performance-ny/public/schedule/detail/51203). The talk was fast-paced and covered a lot of ground including how features we use already (iframes, pre-load etc.) have additional security features that few people use. This was the most practical session of the conference for me, and I need to list all of these out to make sense of it:

### iframes
Iframes are great for performance, kinda.
Over 60% of sites use iframes, yet virtually none of them use the [*sandbox* attribute](https://www.html5rocks.com/en/tutorials/security/sandboxed-iframes/).

### preload, prefetch & preconnect
Preload allows 

https://www.smashingmagazine.com/2016/02/preload-what-is-it-good-for/#how-can-preload-do-better
Types https://fetch.spec.whatwg.org/#concept-request-destination

### content security policy

### service worker

### subresource integrity


## Progressive web apps aren’t all that. Yet.
