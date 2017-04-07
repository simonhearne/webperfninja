---
title: Velocity Europe 2015 - The Good Ones!
date: 2015-11-01 19:54:00 Z
categories:
- '2015'
tags:
- web performance
- velocity
- europe
- amsterdam
- '2015'
comments: true
image:
  feature: ams_hero.jpg
  credit: Velocity at the RAI in Amsterdam
layout: post
excerpt: This post is a review and summary of the talks at Velocity Europe that I attended. I've summarised each talk and given links to the slides, videos and ratings. A <a href="/2015/velocity-europe-2015-report-1/">previous post</a> contains the talks that got a five star review from me. Less than a five star review is not a bad thing, though. Five stars means exceptional, while three stars means the talk had some value.

---

### Continuous Performance - *Stijn Polfliet (CoScale)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/45495) | [Video (5m)](https://www.youtube.com/watch?v=D4tVpzj6BvE) | [Slides (ppt)](http://cdn.oreillystatic.com/en/assets/1/event/134/Continuous%20performance%20Presentation.pptx) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

Stijn's keynote piece was only short (as all sponsored keynotes should be) but he used the time well to highlight CoScale's killer feature.

It appears that CoScale may have solved the biggest problem we have in Web Performance - integrating site speed and business performance data. Everyone in our industry knows that site speed is key to business performance, but we often struggle to spread that message beyond the IT department. By integrating business metrics and performance data we can make better technical decisions and tell a better story about the impact site speed has on our business.

It's worth stating here that [Google Analytics](https://www.google.co.uk/analytics/), [Blue Triangle](http://www.bluetriangletech.com/) and [SOASTA's mPulse](http://www.soasta.com/performance-monitoring/) also collect and report on this data. It remains to be seen who will win over this currently narrow segment of the market.

Stijn lost a star from me as the talk was not as engaging as it could have been and felt like a sales pitch.

----------

### Stranger danger - *Guy Podjarny & Assaf Hefetz (Snyk)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46147) | [Video (14m)](http://www.youtube.com/watch?v=iXA14OFXxZA) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

Guy and Assaf got 15 minutes to demonstrate [Snyk.io](https://snyk.io/) in their (sponsored?) keynote.

Snyk.io (So Now You Know) solves a problem that I didn't know we had - but that I now realise is a huge issue. This problem is that we all use third-party code when we develop applications, and through both direct and indirect dependencies we are continually introducing a huge threat landscape to our applications. Who knows how often vulnerabilities are introduced into open source code, which then get pushed into other code through dependency updates? Snyk.io do.

> The typical Node.js app has over 200 dependencies and 59% of reported vulnerabilities in Maven packages remain unfixed. The mean-time-to-repair (MTTR) for a Maven package vulnerability is *390 days*. This presents a serious threat to projects using these dependencies and at present it is very hard to get any visibility of that threat.

Snyk.io is run from the command line (which calls their remote API service). It can analyse all dependencies in a project and automatically identify *known* vulnerabilities. The killer feature, though, is the ability to automatically patch the vulnerabilities and update your configuration to maintain the patched version in future updates. Very cool.

Snyk.io currently only works with Node.js projects but they will be expanding to other languages shortly. This is definitely a security service to watch.

Guy and Assam lost a star from me as the demo could have been done in less time and the talk felt a little like a hard sell on Snyk.io, even though it sells itself!

----------

### A PaaS for government - *Anna Shipman (Government Digital Service)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46814) | [Blog Post](https://gdstechnology.blog.gov.uk/2015/10/27/looking-at-open-source-paas-technologies/) | [Video (15m)](https://www.youtube.com/watch?v=OLOaq-Xf5zU) | My Rating: ★★★☆☆ | Average Rating: ★★★★☆

Anna took us through the thought process of the Government Digital Service as they introduce a Platform as a Service (PaaS) for government websites.

Anna did a great job in introducing what GDS do and how important it is that people can quickly access their services. A few examples were given such as the ability to book a prison visitation and voter registration.

The government has a problem, though. For each new digital service that goes live (over 800 of them are on the cards!) the project team procures the infrastructure, development environment, database, logging, monitoring etc. This makes for a lot of repetition and a slow time-to-market for new services.

Anna's team are hoping to make the release of a new digital service quick and simple by introducing a Government-wide PaaS. She takes us through the thought process of starting a PaaS at government scale - the challenges that are faced when choosing the correct platform as well as service provider. We were shown a number of candidates and a run-down of pro's and con's to each of them and were promised updates on the [GDS Blog](https://gdstechnology.blog.gov.uk/) as the PaaS is rolled out. I'll certainly be following that closely.

Anna lost a couple of stars from me as the talk was dry and could have focussed more on the human element - who would be helped by this and how much would it affect them? What are the barriers to adoption within the Government?

----------

### Probabilistically sampling a stream of events with a sketch - *Baron Schwartz (VividCortex)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/43888) | [Slides (pdf)](http://cdn.oreillystatic.com/en/assets/1/event/134/Probabilistically%20sampling%20a%20stream%20of%20events%20with%20a%20sketch%20Presentation%201.pdf) | My Rating: ★★★☆☆ | Average Rating: ★★★★☆

In this talk Baron took us on a technical tour of the event sampling algorithm behind [VividCortex](https://www.vividcortex.com/). VividCortex is a cloud based intelligence platform for database system performance and health, it works with all of the big open source database players.

The challenge that Baron described is that the agents installed on customer hardware generate huge volumes of data; sending all of this data back to VividCortex would be infeasible due to both network constraints and the potential resource impact on the customers' host servers.

To overcome this, VividCortex takes a sampling approach to events. While time-series data is sampled once a second, full event traces are sampled on a less frequent basis (about one per hour per category). The challenge here comes in choosing which events to sample. Baron was open about their choices failing a few times and described a number of approaches that were attempted before detailing their chosen methodology.

I felt that the talk became too technical near the end in detailing exactly how the statistical sketch was created, with not enough high-level description of how it can be applied and, more importantly for the audience, where else this kind of sampling could be used. Less technicality in the talk but with a reference to a technical blog post to back it up may have worked better.

Baron lost a couple of stars from me for this reason, as well as the strong feeling of being sold to. It is unfortunate as the general concept is very interesting to me and I would have loved for this to be a five-star talk.

----------

### Fake it until you make it - *Jean-Pierre Vincent (BrainCracking)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44543) | [Slides (ppt)](https://docs.google.com/uc?id=0ByrWN83fytRxQzc3b01wQmJOaEE&export=download) | My Rating: ★★★★☆ | Average Rating: ★★★★☆

In this talk JP uses stories from his clients to show how interface design can overcome some of our inherent performance challenges.

JP's first example was of work he did on a container shipping company. Their challenge was that the web application to book and manage multi-million dollar shipments took sixty seconds to load for Chinese customers. Understandably these customers raised complaints about performance. After doing some work to halve the page load time complaints were still coming in. After all, it was still a thirty second page load!

As a developer with an eye for design, JP found a design solution - he added a spinner to indicate loading on the application page. Complaints dropped a little. He then found another design solution - a five second animation of a seagull flying across the screen. This significantly reduced complaints.

A number of other examples were given of how we, as web developers and designers, should consider performance by design. This is something that [Lara Hogan](http://larahogan.me/design/) has been preaching for quite some time. A new idea to me was using the well-known research showing that we must give feedback within 200ms and show progress within 1000ms. JP showed us how mobile applications in particular are following these rules well. To keep the user engaged they use transition animations between actions, hiding the delay in downloading or preparing content while giving the user a feeling of continuity.

I think JP's conclusions could have been stronger - for example giving your user feedback within 200ms and designing transition pieces to keep the user involved. Overall, though, the talk was very strong and introduced or reinforced a large number of key performance concepts for me.

----------

### Bigger, faster, and more engaging while on a budget - *Nathan Bower (Zillow)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46156) | My Rating: ★★★★☆ | Average Rating: ★★★☆☆

Nathan introduced [Zillow](http://www.zillow.com/) as one of the biggest property websites in the United States. Zillow have faced a number of challenges around web performance, Nathan detailed one challenge in particular as a case study - when the mobile homepage size increased by 12MB.

By using [SpeedCurve](https://speedcurve.com/) and performance budgets Nathan was alerted to this immediately, he even managed to get web developers on the case while he was commuting to work.

It turned out that an A/B testing feature that was not being used was pulling down a large amount of content which was never even rendered.

Nathan's conclusions were that performance budgets are critical, but they must be on the right metrics. His main suggestion was to use the [User Timing API](http://www.stevesouders.com/blog/2014/08/21/resource-timing-practical-tips/) to set custom metrics and track those as well as [SpeedIndex](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) and the more traditional metrics. He also concluded that you can download a whole load of useless data on mobile devices and customers don't care - I'm not sure that I would repeat that one too much!

----------

### Finding bad apples early: Minimizing performance impact - *Arun Kejariwal (Machine Zone)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/43716) | My Rating: ★★★☆☆ | Average Rating: ★★★☆☆

Arun used to work at Twitter where he helped to develop an open source [anomaly detection library](https://github.com/twitter/AnomalyDetection). In this talk he presented how he uses anomaly detection to find bad server nodes in large clusters at his new job with [Machine Zone](https://www.machinezone.com/) (they make the hugely popular mobile game [Game Of War](http://www.gameofwarapp.com/)).

I was unfortunately a little lost by the technicality of the presentation and would have loved more visuals to explain what Arun was talking about - he is obviously an extremely clever chap.

The general idea, I believe, was that he uses clustering on time-series data such as CPU and RAM utilisation across all nodes to identify node behaviour. Once these known-good patterns are learned, anomalies can be detected by comparing the timeseries data of each node against all node clusters. This is performed using the [Euclidean distance measure](https://en.wikipedia.org/wiki/Euclidean_distance) between the data matrices of each cluster-median against the individual node.

The outcome from this work is that the system can now automatically identify nodes which are behaving abnormally in the context of their peers. This allowed Arun to successfully identify a heterogenous server environment where two different types of CPU architecture had been mistakenly installed in nodes in the same cluster.

Arun lost a couple of stars from me as I found it hard to follow the presentation and there were too few conclusions presented. What else can this type of anomaly detection be used for? And will it ever be open source? (The tool discussed in this presentation is different to the open source library mentioned at the beginning).

----------

### Designing for Security Outcomes - *Eleanor Saitta (Dymaxion.org)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/46786) | [Video (18m)](https://www.youtube.com/watch?v=zqnQ0Mvi-as) | [Slides (pdf)](http://cdn.oreillystatic.com/en/assets/1/event/134/Designing%20for%20security%20outcomes%20Presentation.pdf) | My Rating: ★★★☆☆ | Average Rating: ★★★☆☆

Eleanor introduced her keynote by telling us we've got security all wrong, that we focus on technology and not people. She then tells us how we can get better at designing our teams and applications with security in mind.

> Security design is the process of
understanding user culture, goals,
and workflows, organizational
technical capabilities, and adversary
capabilities and dispositions and
synthesizing a satisficing solution.

Eleanor suggests that we should all be building thorough threat models (rather than threat lists) at the very early stages of projects. This will allow us to capture potential security concerns early, as we will have a better understanding of the potential adversaries we face.

I'm afraid I got lost at a few points in Eleanor's keynote, the slides were occasionally distracting and some un-introduced security terms threw me off. That's why she lost a couple of stars from me.

----------

### A day in the life - An immersive data experience - *David Boloker (IBM Corporation)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/47746) | [Video (10m)](https://www.youtube.com/watch?v=6vMR6p-ff9U) | My Rating: ★★★☆☆ | Average Rating: ★★★★☆

David had a hard job in his sponsored keynote. He started by introducing the limitations we currently have with our Human-Computer Interaction (HCI) and that we need a more natural way to communicate with machines.

To demonstrate this David quickly switched into a live demonstration of a piece of conversational software. The demo was unfortunately contrived and awkward; the speech recognition did not work well in the keynote setting, the feedback from the software was slow and machine-like and the quality of data was not much better than you would get from Siri.

----------

### Thinking about thinking (about people) - *Courtney W. Nash (O'Reilly)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/48025) | [Video (10m)](https://www.youtube.com/watch?v=tkJtr6xJp4g) |  My Rating: ★★★★☆ | Average Rating: ★★★★☆

Courtney's background is in cognitive science and that really comes across in this keynote.

I think Courtney's general point is that humans are not inherently sensible or unbiased. We are weird creatures that do not follow the rules. An example was given of a 'shared space' created in a town which mixed pedestrians, cyclists and drivers with no traffic lights or stop signs. This forced people to be more considerate of those around them and in-turn increased safety.

This 'shared space' was eventually reverted, though. Even though empirical safety had increased significantly, the residents still *felt* that the junction was less safe and campaigned against it.

Courtney then related this to the web performance industry by citing an [article](https://www.uie.com/articles/download_time/) published in User Interface Engineering in 2001. The article states that if a user achieves what they set out to do on a website, they perceive it as 'fast'. This perception of speed, however, has no correlation to the actual speed of the site! Courtney's conclusion from this is that we need to measure and monitor better metrics, [time to first tweet](http://blog.alexmaccaw.com/time-to-first-tweet) was referenced.

Courtney then took a turn towards operations for a conclusion that everyone should share responsibility for the uptime of a site or application, where uptime is measured as the ability of a customer to complete their action.

----------

### Measuring the performance of single page web applications - *Philip Tellis & Nic Jansma (SOASTA)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44019) |  My Rating: ★★★★☆ | Average Rating: ★★★★☆

Philip and Nic work on SOASTA's Real User Measurement (RUM) product mPulse. In this talk they gave a run-down on the work they are doing with [boomerang](https://github.com/lognormal/boomerang/) to improve the data captured on single-page applications (SPAs).

SPAs give us a fundamental challenge when it comes to monitoring - the old paradigm of clicking a link causing a page navigation which can be tracked is no more. When SOASTA enabled SPA measurement for one client the amount of datapoints collected increased four-fold!

The work Philip and Nic are doing is around developing [plugins](https://github.com/lognormal/boomerang/tree/soasta-2015/plugins) for boomerang which instrument the network activity created by SPAs.

The conclusion is that browsers need to catch up with vendors - it should not be so difficult to monitor and measure real users.

----------

### Open components as microservices in the front-end world - *Matteo Figus (OpenTable)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44289) |  My Rating: ★★★★☆ | Average Rating: ★★★☆☆

In this talk Matteo introduced his open source project [open components](https://github.com/opentable/oc). Matteo describes how difficult it is to develop a website in the complex environment at OpenTable, with many engineers based out of multiple countries all working on the same site.

To solve the challenges faced with front-end development at OpenTable, they decided to break the development down to micro-sites. By utilising common components and removing interdependencies the developers can now rapidly develop these micro-sites and push to live indepently of each other.

Open components provides a registry and commandline service to create front-end components.

----------

### A real-life account of moving 100% to a public cloud - *Julien Simon (AWS) & Antoine Guy (Viadeo)*

#### [Description](http://velocityconf.com/devops-web-performance-eu-2015/public/schedule/detail/44042) |  My Rating: ★★★☆☆ | Average Rating: ★★★★☆

Julien and Antoine were part of the team that migrated [Viadeo](http://gb.viadeo.com/en/) to a public cloud stack. In this talk they describe the technical process they went through to get the site successfully migrated.

The main outcome of the migration was the move to [CloudFormation](https://aws.amazon.com/cloudformation/) to automate Infrastructure as Code. 
