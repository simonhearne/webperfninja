---
layout: post
title:  "Velocity Europe 2015 - Thursday Review"
date:   2015-11-01 19:54:00
category: 2015
tags: [web performance, velocity, europe, amsterdam, 2015]
comments: true
image:
  feature: "ams_hero.jpg"
  credit: Velocity at the RAI in Amsterdam
---

This post is a summary of the talks that I attended at the first day of Velocity in Amsterdam in 2015. Partly for my own reference, I've briefly described each talk that I attended, links to any descriptions, slides and videos as well as the ratings from myself and the average rating for the talk.

A second post will follow for the second day, and I will also add a review of the WebPerfDays unconference day which followed the main conference.

##The Physical Web is a Speed Issue - *Scott Jenson (Google)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/45231) | [Video (18m)](https://www.youtube.com/watch?v=7H_E_ZbFAn0) | My Rating: ★★★★★ | Average Rating: ★★★★☆

Scott's keynote was probably the highlight of this Velocity for me. He discusses how the web will change over the next few years with the development of the advent of the Physical Web and the Internet Of Things.

Scott used a number of examples to show how this will affect our daily lives, with a parking meter being the clearest demonstration.

Imagine a parking meter which has a light-weight web server and low-energy bluetooth. The bluetooth (or other low-energy, low-range wireless technology) continuously publishes a unique URL for the web server. You park your car and pull out your phone, in your notification tray this URL has silently appeared. You click on the link and immediately load a payment page for the parking meter, one tap and you've got an hour's worth of parking and the meter screen immediately updates.

This sounds pretty futuristic, but almost all of the technology we need is already in place. The one part that's missing is the silent notifications - broadcasting a link that nearby devices can pick up but without irritating every passer-by (like iBeacon). Scott's team at Google is working on this very challenge, there is an open source repository with a functioning Chrome extensios on iPhone (but not Android!) on [GitHub](https://github.com/google/physical-web). This technology is based on Google's open Bluetooth low-energy protocol [Eddystone](https://github.com/google/eddystone).

The title of Scott's talk took me a while to decipher: "The Physical Web is a Speed Issue". By this I think he means that the Physical Web will make our day-to-day lives more 'speedy'. This will be achieved by automating link sharing, thus making tedious tasks such as paying for parking or interacting with every-day items much easier and faster. In order for this to work, though, we need *fast mobile web applications*.

We cannot and will not install an application for every light bulb, parking meter or door lock which makes up the Physical Web. Technologies such as [service worker](https://github.com/slightlyoff/ServiceWorker/) and [quic](https://www.chromium.org/quic) are going to be essential to make the Physical Web fast and, more important, accessible. 

> The Physical Web is like a really awesome QR Code

This talk really hit home for me. As someone who runs two QR Code services ([QR Explore](https://qrexplore.com) and [ThisQR](http://thisqr.com)) I am more than familiar with the drawbacks of QR Codes in western society - no one wants to be seen taking a picture of a poster! This means that QR Codes work best in a closed environment such as a factory (which is why they were invented) or a science center. The potential for having QR Code-like functionality (link discovery) without the awkward scanning issue is an absolute game-changer.

----------

##Continuous Performance - *Stijn Polfliet (CoScale)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/45495) | [Video (5m)](https://www.youtube.com/watch?v=D4tVpzj6BvE) | [Slides (ppt)](http://cdn.oreillystatic.com/en/assets/1/event/134/Continuous%20performance%20Presentation.pptx) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

Stijn's keynote piece was only short (as all sponsored keynotes should be) but he used the time well to highlight CoScale's killer feature.

It appears that CoScale may have solved the biggest problem we have in Web Performance - integrating site speed and business performance data. Everyone in our industry knows that site speed is key to business performance, but we often struggle to spread that message beyond the IT department. By integrating business metrics and performance data we can make better technical decisions and tell a better story about the impact site speed has on our business.

It's worth stating here that [Google Analytics](https://www.google.co.uk/analytics/), [Blue Triangle](http://www.bluetriangletech.com/) and [SOASTA's mPulse](http://www.soasta.com/performance-monitoring/) also collect and report on this data. It remains to be seen who will win over this currently narrow segment of the market.

Stijn lost a star from me as the talk was not as engaging as it could have been and felt like a sales pitch.

----------

##Stranger danger - *Guy Podjarny & Assaf Hefetz (Snyk)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46147) | [Video (14m)](http://www.youtube.com/watch?v=iXA14OFXxZA) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

Guy and Assaf got 15 minutes to demonstrate [Snyk.io](https://snyk.io/) in their (sponsored?) keynote.

Snyk.io (So Now You Know) solves a problem that I didn't know we had - but that I now realise is a huge issue. This problem is that we all use third-party code when we develop applications, and through both direct and indirect dependencies we are continually introducing a huge threat landscape to our applications. Who knows how often vulnerabilities are introduced into open source code, which then get pushed into other code through dependency updates? Snyk.io do.

> The typical Node.js app has over 200 dependencies and 59% of reported vulnerabilities in Maven packages remain unfixed. The mean-time-to-repair (MTTR) for a Maven package vulnerability is *390 days*. This presents a serious threat to projects using these dependencies and at present it is very hard to get any visibility of that threat.

Snyk.io is run from the command line (which calls their remote API service). It can analyse all dependencies in a project and automatically identify *known* vulnerabilities. The killer feature, though, is the ability to automatically patch the vulnerabilities and update your configuration to maintain the patched version in future updates. Very cool.

Snyk.io currently only works with Node.js projects but they will be expanding to other languages shortly. This is definitely a security service to watch.

Guy and Assam lost a star from me as the demo could have been done in less time and the talk felt a little like a hard sell on Snyk.io, even though it sells itself!

----------

##Discovering Operations Expertise - *John Allspaw (Etsy)*
##[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/47779) | [Video (20m)](https://www.youtube.com/watch?v=OJ21jwJThq4) | [Thesis (pdf)](http://bit.ly/AllspawThesis) | My Rating: ★★★★★ | Average Rating: ★★★★☆

John's keynote was a very brief summary of his work towards a thesis in Human Factors Engineering.

We often focus on analysing failures to find out what has gone wrong. John's point was that we need to focus on success as well in order to find out why something has not gone wrong. No matter how much we automate, humans will always be the lynchpin of success or failure in deployment; if we analyse what comes together to make successful human behaviour then we can improve success rate at the individual level.

John suggests that in order to increase efficiency, especially in times of crisis, we also need to find out what engineers do in the event of failure - what are the rules of thumb that are followed? Once we know that, we can analyse and improve our processes.

This talk was a refreshing change from the technical focus of the conference, instead proposing that as humans are the critical factors in all that we do, so we must focus there first.

----------

##A PaaS for government - *Anna Shipman (Government Digital Service)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46814) | [Blog Post](https://gdstechnology.blog.gov.uk/2015/10/27/looking-at-open-source-paas-technologies/) | [Video (15m)](https://www.youtube.com/watch?v=OLOaq-Xf5zU) | My Rating: ★★★☆☆ | Average Rating: ★★★★☆

Anna took us through the thought process of the Government Digital Service as they introduce a Platform as a Service (PaaS) for government websites.

Anna did a great job in introducing what GDS do and how important it is that people can quickly access their services. A few examples were given such as the ability to book a prison visitation and voter registration.

The government has a problem, though. For each new digital service that goes live (over 800 of them are on the cards!) the project team procures the infrastructure, development environment, database, logging, monitoring etc. This makes for a lot of repetition and a slow time-to-market for new services.

Anna's team are hoping to make the release of a new digital service quick and simple by introducing a Government-wide PaaS. She takes us through the thought process of starting a PaaS at government scale - the challenges that are faced when choosing the correct platform as well as service provider. We were shown a number of candidates and a run-down of pro's and con's to each of them and were promised updates on the [GDS Blog](https://gdstechnology.blog.gov.uk/) as the PaaS is rolled out. I'll certainly be following that closely.

Anna lost a couple of stars from me as the talk was dry and could have focussed more on the human element - who would be helped by this and how much would it affect them? What are the barriers to adoption within the Government?

----------

##Probabilistically sampling a stream of events with a sketch - *Baron Schwartz (VividCortex)*
##[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/43888) | [Slides (pdf)](http://cdn.oreillystatic.com/en/assets/1/event/134/Probabilistically%20sampling%20a%20stream%20of%20events%20with%20a%20sketch%20Presentation%201.pdf) | My Rating: ★★★☆☆ | Average Rating: ★★★★☆

In this talk Baron took us on a technical tour of the event sampling algorithm behind [VividCortex](https://www.vividcortex.com/). VividCortex is a cloud based intelligence platform for database system performance and health, it works with all of the big open source database players.

The challenge that Baron described is that the agents installed on customer hardware generate huge volumes of data; sending all of this data back to VividCortex would be infeasible due to both network constraints and the potential resource impact on the customers' host servers.

To overcome this, VividCortex takes a sampling approach to events. While time-series data is sampled once a second, full event traces are sampled on a less frequent basis (about one per hour per category). The challenge here comes in choosing which events to sample. Baron was open about their choices failing a few times and described a number of approaches that were attempted before detailing their chosen methodology.

I felt that the talk became too technical near the end in detailing exactly how the statistical sketch was created, with not enough high-level description of how it can be applied and, more importantly for the audience, where else this kind of sampling could be used. Less technicality in the talk but with a reference to a technical blog post to back it up may have worked better.

Baron lost a couple of stars from me for this reason, as well as the strong feeling of being sold to. It is unfortunate as the general concept is very interesting to me and I would have loved for this to be a five-star talk.

----------

##Fake it until you make it - *Jean-Pierre Vincent (BrainCracking)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44543) | [Slides (ppt)](https://docs.google.com/uc?id=0ByrWN83fytRxQzc3b01wQmJOaEE&export=download) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

In this talk JP uses stories from his clients to show how interface design can overcome some of our inherent performance challenges.

JP's first example was of work he did on a container shipping company. Their challenge was that the web application to book and manage multi-million dollar shipments took sixty seconds to load for Chinese customers. Understandably these customers raised complaints about performance. After doing some work to halve the page load time complaints were still coming in. After all, it was still a thirty second page load!

As a designer, JP found a design solution - he added a spinner to indicate loading on the application page. Complaints dropped a little. He then found another design solution - a five second animation of a seagull flying across the screen. This significantly reduced complaints.

A number of other examples were given of how we, as web developers and designers, should consider performance by design. This is something that [Lara Hogan](http://larahogan.me/design/) has been preaching for quite some time. A new idea to me was using the well-known research showing that we must give feedback within 200ms and show progress within 1000ms. JP showed us how mobile applications in particular are following these rules well. To keep the user engaged they use transition animations between actions, hiding the delay in downloading or preparing content while giving the feeling of continuity.

I think JP's conclusions could have been stronger - for example giving your user feedback within 200ms and designing transition pieces to keep the user involved. Overall, though, the talk was very strong and introduced or reinforced a large number of key performance concepts for me.

----------

##Bigger, faster, and more engaging while on a budget - *Nathan Bower (Zillow)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46156) | My Rating: ★★★★☆ | Average Rating: ★★★☆☆

Nathan introduced [Zillow](http://www.zillow.com/) as one of the biggest property websites in the United States. Zillow have faced a number of challenges around web performance, Nathan detailed one challenge in particular as a case study - when the mobile homepage size increased by 12MB.

By using [SpeedCurve](https://speedcurve.com/) and performance budgets Nathan was alerted to this immediately, he even managed to get web developers on the case while he was commuting to work.

It turned out that an A/B testing feature that was not being used was pulling down a large amount of content which was never even rendered.

Nathan's conclusions were that performance budgets are critical, but they must be on the right metrics. His main suggestion was to use the [User Timing API](http://www.stevesouders.com/blog/2014/08/21/resource-timing-practical-tips/) to set custom metrics and track those as well as [SpeedIndex](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) and the more traditional metrics. He also concluded that you can download a whole load of useless data on mobile devices and customers don't care - I'm not sure that I would repeat that one too much!

----------

##Finding bad apples early: Minimizing performance impact - *Arun Kejariwal (Machine Zone)*
###[Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/43716) | My Rating: ★★★☆☆ | Average Rating: ★★★☆☆

Arun used to work at Twitter where he helped to develop an open source [anomaly detection library](https://github.com/twitter/AnomalyDetection). In this talk he presented how he uses anomaly detection to find bad server nodes in large clusters at his new job with [Machine Zone](https://www.machinezone.com/) (they make the hugely popular mobile game [Game Of War](http://www.gameofwarapp.com/)).

I was unfortunately a little lost by the technicality of the presentation and would have loved more visuals to explain what Arun was talking about - he is obviously an extremely clever chap.

The general idea, I believe, was that he uses clustering on time-series data such as CPU and RAM utilisation across all nodes to identify node behaviour. Once these known-good patterns are learned, anomalies can be detected by comparing the timeseries data of each node against all node clusters. This is performed using the [Euclidean distance measure](https://en.wikipedia.org/wiki/Euclidean_distance) between the data matrices of each cluster-median against the individual node.

The outcome from this work is that the system can now automatically identify nodes which are behaving abnormally in the context of their peers. This allowed Arun to successfully identify a heterogenous server environment where two different types of CPU architecture had been mistakenly installed in nodes in the same cluster.

Arun lost a couple of stars from me as I found it hard to follow the presentation and there were too few conclusions presented. What else can this type of anomaly detection be used for? And will it ever be open source? (The tool discussed in this presentation is different to the open source library mentioned at the beginning).