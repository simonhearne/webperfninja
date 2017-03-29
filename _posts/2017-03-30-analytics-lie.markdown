---
title: Your Analytics is Lying to You
date: 2017-03-30 00:00:00 Z
categories:
- '2017'
comments: true
image:
  feature: "../uploads/analytics-hero.png"
toc: true
excerpt: You can't rely on your web analytics for performance data, oh and it's underestimating traffic from old devices.
layout: post
published: true
---

tl;dr: your analytics is almost certainly rubbish at reporting site speed data, and definitely under-reports bounce rate and traffic from old devices.

## The site speed fallacy

In a recent webinar, Andy Davies and I asked a poll of the attendees: where do you get your performance data from? Bear in mind that the majority of the attendees on the webinar were from Ecommerce or Digital Management. The results were just about what we were expecting, the majority of attendees use web analytics to get performance data:

<figure align="center">
<img style="max-width:80%;" src="/uploads/poll-analytics.png"/>
<figcaption>Poll showing that 58% use web analytics to get site speed data</figcaption>
</figure>

A further 29% of attendees use synthetic monitoring as their source of site speed data. While synthetic monitoring is great for measuring operational performance and tracking changes over time, it gives little indication of the real user experience. Only 2% of attendees stated that they use real user monitoring.

Using analytics for site speed is logical, if you have a website you will have analytics. Access to products like Google Analytics is widespread throughout an organisation, and it provides reporting on site speed data. Google Analytics (GA) is actually the best we've seen for reporting site speed. You can view multiple timing metrics and segment by device type or location. Adobe Analytics has no default site speed data, you have to manually add it to the analytics code, once it's being collected there is very little you can do with it.

GA's site speed data is flawed. The data is sampled, limited by default to [no more than 1% of pageviews](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#siteSpeedSampleRate). This sample rate can be changed to 100%, although I've not seen that done on a high-traffic site.
Even if GA collects 100% of site speed data, it cannot be correlated with any other metric. The speed data is aggregated by time, and not linked with sessions. As such it is impossible to determine the user experience of a whole session, or indeed to correlate speed with likelihood to convert.

Most of my job as a performance consultant is convincing companies that site speed is critical to their business, GA does not make that easy!

## Phantom bounces

Anyway, so you've changed your sampling rate and got 100% of your pageviews sending site speed data. The average page load time is seven seconds, seems pretty slow. Bounce rate is just touching 50%, that seems pretty bad too.
It's scary to think about, but your bounce rate is likely *much* higher than 50%. Bounces are sessions which have only one pageview, they don't count sessions which have less than one pageview... bear with me.

A recent [study by Google](https://www.doubleclickbygoogle.com/articles/mobile-speed-matters/) showed, by comparing DoubleClick ad clicks and Google Analytics pageviews, that 53% of ad clicks never result in a pageview when the page has a load time of over three seconds. Your analytics shows you that your mobile page load time is eight seconds, so how many users with the intention of loading your site *never* result in a pageview?

These non-pageviews are *phantom bounces*. They don't appear anywhere in your analytics, but they could be a significant proportion of your traffic driven by marketing campaigns. What's worse, your marketing budget will be spent on traffic which may never reach your landing pages.

Most of my clients base their device testing strategy on their analytics. I vividly remember a story I was told by an employee at a large UK retailer: when first joining the mobile team as a contract resource she questioned why there was no testing on the first generation iPad. She was told that their analytics showed no traffic from such an old device (three years after it was launched) so there was no need to test. The sceptical contractor got our her very-much-still-working first-gen iPad and loaded the homepage. Safari crashed.

This is a textbook case of the [tail wagging the dog](https://en.wiktionary.org/wiki/tail_wagging_the_dog).

# Solutions
Right, that's enough of problems. How do we go about getting the right information?

## Analytics

There's little that one can do to improve your analytics. With GA you can increase the site speed sample rate, but the data still doesn't have much value. It's the same with Adobe Analytics. Unfortunately I think it's currently necessary to have separate performance and analytics products.

## Phantom bounces

Phantom bounces are an interesting challenge. From the DoubleClick study we know that there is a disparity between the clicks being logged and the pages being loaded. The flow goes something like this, assuming a click from Google's SERP:

 - User clicks a link (looks like your site, is actually Google)
 - Google logs the click, redirects user to your site
 - User's browser makes a request for your site
 - Your site responds with some HTML
 - HTML, CSS, JavaScript are processed
 - Page loads
 - Analytics fires

 Ideally, we would get data from the first step - how many people make the intention to load the page. This information is extremely hard to get, although an advertising provider should report on the number of clicks. If you have a good URL strategy then you might be able to do your own DoubleClick-style study, correlating ad clicks with pageviews.

 It's possible to correlate page requests with pageviews. Web server or CDN logs can be plotted against reported page impressions to determine the analytics loss. Further correlation can be run against the useragent of the requests to identify devices which are more underreported in analytics than others.
