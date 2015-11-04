---
layout: post
title:  "Velocity Europe 2015 - My Allstars"
date:   2015-11-01 19:54:00
category: 2015
tags: [web performance, velocity, europe, amsterdam, 2015]
comments: true
image:
  feature: "ams_hero_5.jpg"
  credit: Velocity at the RAI in Amsterdam
---

This post is a review and summary of the talks at Velocity Europe that got a 5 star review from me. I've summarised each talk and given links to the slides, videos and ratings.

I hope that this will help anyone who did not get a chance to attend the conference to get a taste of the exceptional talks that I was lucky enough to see.

A [further post](/2015/velocity-europe-2015-report-2/) contains the talks that didn't quite get a five star review from me.

----------

###The Physical Web is a Speed Issue - *Scott Jenson (Google)*

####[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/45231) | [Video (18m)](https://www.youtube.com/watch?v=7H_E_ZbFAn0) | My Rating: ★★★★★ | Average Rating: ★★★★☆

Scott's keynote was probably the highlight of this Velocity for me. He discusses how the web will change over the next few years with the advent of the Physical Web and the Internet Of Things.

Scott used a number of examples to show how this will affect our daily lives, with a parking meter being the clearest demonstration.

Imagine a parking meter which has a light-weight web server and low-energy bluetooth. The bluetooth (or other low-energy, low-range wireless technology) continuously publishes a unique URL for the web server. You park your car and pull out your phone, in your notification tray this URL has silently appeared. You click on the link and immediately load a payment page for the parking meter, one tap and you've got an hour's worth of parking and the meter screen immediately updates.

This sounds pretty futuristic, but almost all of the technology we need is already in place. The one part that's missing is the silent notifications - broadcasting a link that nearby devices can pick up but without irritating every passer-by (like iBeacon). Scott's team at Google is working on this very challenge, there is an open source repository with a functioning Chrome extensios on iPhone (but not Android!) on [GitHub](https://github.com/google/physical-web). This technology is based on Google's open Bluetooth low-energy protocol [Eddystone](https://github.com/google/eddystone).

The title of Scott's talk took me a while to decipher: "The Physical Web is a Speed Issue". By this I think he means that the Physical Web will make our day-to-day lives more 'speedy'. This will be achieved by automating link sharing, thus making tedious tasks such as paying for parking or interacting with every-day items much easier and faster. In order for this to work, though, we need *fast mobile web applications*.

We cannot and will not install an application for every light bulb, parking meter or door lock which makes up the Physical Web. Technologies such as [service worker](https://github.com/slightlyoff/ServiceWorker/) and [quic](https://www.chromium.org/quic) are going to be essential to make the Physical Web fast and, more important, accessible. 

> The Physical Web is like a really awesome QR Code

This talk really hit home for me. As someone who runs two QR Code services ([QR Explore](https://qrexplore.com) and [ThisQR](http://thisqr.com)) I am more than familiar with the drawbacks of QR Codes in western society - no one wants to be seen taking a picture of a poster! This means that QR Codes work best in a closed environment such as a factory (which is why they were invented) or a science center. The potential for having QR Code-like functionality (link discovery) without the awkward scanning issue is an absolute game-changer.

----------

###Discovering Operations Expertise - *John Allspaw (Etsy)*

####[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/47779) | [Video (20m)](https://www.youtube.com/watch?v=OJ21jwJThq4) | [Thesis (pdf)](http://bit.ly/AllspawThesis) | My Rating: ★★★★★ | Average Rating: ★★★★☆

John's keynote was a very brief summary of his work towards a thesis in Human Factors Engineering.

We often focus on analysing failures to find out what has gone wrong. John's point was that we need to focus on success as well in order to find out why something has not gone wrong. No matter how much we automate, humans will always be the lynchpin of success or failure in deployment; if we analyse what comes together to make successful human behaviour then we can improve success rate at the individual level.

John suggests that in order to increase efficiency, especially in times of crisis, we also need to find out what engineers do in the event of failure - what are the rules of thumb that are followed? Once we know that, we can analyse and improve our processes.

This talk was a refreshing change from the technical focus of the conference, instead proposing that as humans are the critical factors in all that we do, so we must focus there first.

----------

###Ensuring a high performing web for the next billion people - *Bruce Lawson (Opera ASA)*

####[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44920) | [Video (20m)](https://www.youtube.com/watch?v=f6As5HEkG5E) | My Rating: ★★★★★ | Average Rating: ★★★★★

The highest rated talk of Velocity. I saw Bruce give this talk at Velocity Santa Clara earlier this year and it has got even better.

Few of us consider proxy browsers when we develop websites, but Opera Mini alone serves over 350 Million customers. By developing Javascript-rich websites or by using icon fonts we may be excluding a huge portion of our future market.


----------

###One year later: How Marks & Spencer revolutionized PerfOps after Velocity 2014 - *Andrew Neilson (M&S)*

####[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44100) |  My Rating: ★★★★★ | Average Rating: ★★★★☆

Andy runs PerfOps and marksandspencer.com - a large UK retailer that does 20% of its business online. In this talk he described how Velocity Europe 2014 inspired him to refactor performance operations at M&S.

Andy gave a practical run-down of the tools and metrics that M&S use to track performance with a number of examples to illustrate his points.

A key turning point for the business was when SpeedCurve showed a huge increase in third-party calls on the M&S homepage. This led Andy to investigate what had happened using my [requestmap](http://requestmap.webperf.tools/) and discovered that a third-party service had started calling more third-party domains. This discovery led to a piece of analysis showing that third-parties were responsible for 50% of the load time on the homepage.

