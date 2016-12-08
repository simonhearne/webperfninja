---
title: Three WebPerf Takeaways from Velocity Europe
date: 2016-11-08 13:08:00 Z
categories:
- '2016'
comments: true
image:
  feature: "../uploads/velocity_hillary_hero.jpg"
layout: post
---

Velocity Amsterdam has just come to a close. Here are the three key things that I am taking away from the two days of sessions.

## 1) Performance KPIs are broken

This was one of the themes that ran like an undercurrent through the whole conference, starting with [Steve Souders](https://twitter.com/souders) at WebPerfDays talking about the death of window.onload for performance measurement. It's been known for a while that the onload event is flawed for measuring performance, but it has been universal across browsers so was the lowest friction measure. The problem with measuring onload is that the number can be [gamed](http://www.leanblog.org/tag/gaming-the-numbers/). Better numbers can be achieved by moving content around, while the measure can also be influenced by third-party content. The onload does not necessarily bare any relation to user experience, especially with JavaScript-driven websites.

There are a great many alternatives to the onload event for measuring performance. [Speed Index](https://sites.google.com/a/webpagetest.org/docs/using-webpagetest/metrics/speed-index) measures the average time at which parts of the page are displayed in synthetic tests. [User timings](http://www.webperformance.io/custom-user-timings) can measure specific events such as time-to-first-interaction for real user monitoring. None of these are a silver bullet: Speed Index is impacted by cookie banners and modals, and is dependent on test speed and viewport size. User timings have to be carefully thought out and defined for specific page types, making them labour intensive.

> > recommendations and statistics are objective measures of performance, but user perception is not mathematics

[Denys Mishunov](https://twitter.com/mishunov) also spoke at WebPerfDays, he says that "recommendations and statistics are objective measures of performance, but user perception is not mathematics". Denys had some great examples of objectively fast experiences that had a poor user experience, such as a coin counting machine that users didn't trust because it [counted coins too quickly](http://www.90percentofeverything.com/2010/12/16/adding-delays-to-increase-perceived-value-does-it-work/). He extended this concept to the idea of passive- vs active-waiting: we can trick the user into thinking an interaction is just the right speed by manipulating the experience. [Optimistic UIs](https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/) are an example of using this in the wild. This concept makes measuring simple timing points of pages almost totally irrelevant, instead we need to measure when the user thought that the key event occurred, the delay until it actually occurred and the failure rate of the optimistic UI interaction.

One of the questions asked by the audience after [Kevin Bowman](https://twitter.com/__kb)'s great talk about [surviving big events](http://conferences.oreilly.com/velocity/devops-web-performance-eu/public/schedule/detail/53557) was 'what is the uptime SLA for Sky Betting'. Kevin's response was that they didn't have an official SLA, everyone just tries their best and they trust others to do the same. From my experience, having an SLA leads to gaming the numbers. This is especially true when there are incentives (i.e. a financial bonus) linked to the reported figure.

> > Targets always result in gaming

Gaming the numbers certainly is not restricted to web performance. The UK National Health System has been highlighted as an organisation where KPIs have led to poor standards of care, leading to [unnecessary patient deaths](http://www.nationalhealthexecutive.com/Health-Care-News/nhs-performance-management-putting-standards-of-care-at-risk), even though the care givers give great concern to the welfare of their patients. KPIs are easy for senior stakeholders to set and measure - on paper they are the ideal way to get visibility into performance. Unfortunately static goals are open to abuse through manipulating the numbers in any number of ways.

To improve performance we should enable teams to be successful, to measure their own performance and set their own definitions of success.


## 2) Team success = business success


This was a positive theme that ran through a lot of the talks at velocity. We must enable our teams to do their jobs, let them make their own decisions and remove micro-management.
A great example of this was given by Kevin from Sky Betting. In the run up to the biggest event in SkyBet's calendar, they knew it was going to be tough. Kevin even said "we knew we were going to run out of compute resource, we just didn't know where". Team dynamics are critical in order to survive an event where just minutes of downtime can cost £100,000s of customer bets. SkyBet has cross-team 'squads', each of which has a responsibility on the production system. These squads are self-managing, so when something goes wrong they just get on and fix it. There were some close calls during the big event, with the platform almost coming to a stand-still. Kevin believes that the trust and independence of the squads allowed the issues to be resolved as quickly as possible, without large-scale war rooms which would have wasted valuable time.

> > Successful teams are trusted and manage themselves.

[Sarah Wells](https://twitter.com/sarahjwells) from the FT emphasized the importance of enabling teams to clearly state their key goal(s). Without clear, agreed upon direction, teams will never realise their maximum potential. As part of this goal, teams at the FT are empowered to choose whatever tools and processes they think will be the best fit for their problems. In order to maintain supportability these teams are then responsible for supporting their chosen technologies 24x7, if they're not already covered by first-line support.

[Arnoud Vermeer](https://twitter.com/funzoneq) from Leaseweb described the journey from [waterfall to agile developement](http://conferences.oreilly.com/velocity/devops-web-performance-eu/public/schedule/detail/52562). One of the key concepts that Arnoud attributes to the success of their agile methodology is autonomous, empowered teams. Each team is responsible for one product. That responsibility extends from planning through development to in-live support. This enabled Leaseweb to produce predictable development, with priorities based on business value. The development roadmap is transparent to the whole company, with all employees involved in strategic direction.

To keep Leaseweb on track, there is a shared dashboard which shows the results of an anonymous post-sprint retrospective survey. This gives an early indication of when team dynamics begin to fail.

<figure align="center">
<img style="max-width:90%;" src="/uploads/team_dashboard.png"/>
<figcaption>Leaseweb's Retro Dashboard (<a href="http://cdn.oreillystatic.com/en/assets/1/event/167/The%20Anarchist%20Cookbook_%20DevOps%20and%20Agile%20recipes%20for%20blowing%20up%20the%20waterfall%20Presentation.pdf">source</a>)</figcaption>
</figure>

[Astrid Atkinson](https://twitter.com/shinynew_oz) listed seven factors which lead to successful teams in her keynote, which by proxy lead to business success:

 * Diversity is strength - only with a diverse set of personalities can you truly develop strong ideas
 * The best teams are inclusive - all ideas should be treated with respect and openness
 * Seek understanding, not skills - when hiring, look for candidates who will be a good personal fit
 * Give power away - empower teams to make the right (or wrong) choices
 * Create safety - there should be no fear of speaking out, even to the CEO of the company
 * Mission matters - the company, team and individual must all have a clear common mission


## 3) We are not using great Web features


There are a number of great Web features that are available to us today, yet few websites are utilising them. One example is the challenge of under-utilised bandwidth: currently, there is a delay while the browser downloads and parses the HTML document, discovers a ```<link rel='stylesheet'>``` directive and requests the CSS asset(s) required to render the page.

This process takes time. This delay is unnecessary as the server already knows what assets are critical to render the page!

Enter ```<link rel='preload'>```.

Preload is an HTML directive or HTTP header which hints to the browser that the linked asset should be pre-emptively loaded, as soon as possible. As an HTML directive it doesn't offer much of a performance benefit in the described scenario. As an HTTP header however, it can offer a performance gain: the browser is made aware of a critical asset before the HTML is even downloaded.

HTTP/2 takes this paradigm one step further. [HTTP/2 Server Push](https://www.igvita.com/2013/06/12/innovating-with-http-2.0-server-push/) allows the server to actively push the asset to the browser. Cloudflare's CDN currently [implements this automatically](https://blog.cloudflare.com/announcing-support-for-http-2-server-push-2/) when it sees the preload header.

[Colin Bendell](https://twitter.com/colinbendell) of Akamai spoke about the [promise of Push](http://conferences.oreilly.com/velocity/devops-web-performance-eu/public/schedule/detail/53584). Although there is still some work to do on mainstream support (test your browser using Colin's [canipush.com](https://canipush.com)), we can deploy Push now. Pushing CSS shows performance gains, while pushing anything else might actually make things worse. ```<link rel='preload'>``` may still be the best option for WebFonts, for example.

<figure align="center">
<img style="max-width:80%;" src="/uploads/push.png"/>
<figcaption>Potential win area for Push</figcaption>
</figure>

Another technology mentioned a lot, again, was Progressive Web Apps. The magical combination of [web app manifests](https://developers.google.com/web/updates/2014/11/Support-for-installable-web-apps-with-webapp-manifest-in-chrome-38-for-Android), [service worker](https://jakearchibald.com/2014/using-serviceworker-today/) and [web push notifications](https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/) which give us a near-native web app experience on Android devices. The fundamental technologies for PWAs have [been around since mid-2015](https://infrequently.org/2015/06/progressive-apps-escaping-tabs-without-losing-our-soul/), and yet adoption is extremely low. Only 0.5% of mobile pages tested by HTTP Archive include a ```manifest``` object.

[Jason Grigsby](https://twitter.com/grigs) gave an [interesting keynote](http://conferences.oreilly.com/velocity/devops-web-performance-eu/public/schedule/detail/54697) about PWAs. He explained that every step towards a PWA [makes sense on its own](https://cloudfour.com/thinks/progressive-web-apps-simply-make-sense/). As such it's shocking that web app manifests, the first step towards PWAs, have such a low penetration.

From speaking with my clients, it seems that there is a hesitance to 'jump in to bed' with PWAs. There are questions around the lack of support on iPhones as well as the feared erosion of native application market share. However, as Jason said, each step makes sense on its own. I recommend that my clients start work towards PWAs with a web app manifest and start to investigate the potential of service worker.

## BONUS - Empathise with your audience

One of the key differentiating factors for the presentations I attended was whether the speaker empathised with their audience or not. By that I mean there were some speakers who had clearly thought about the Velocity audience and showed empathy for their pains and challenges at the very beginning of their talks. There were other speakers who appeared to be speaking for their own benefit, and had not thought about why the audience might want to hear what they have to say.

I'll do my best to keep that in mind when speaking, I hope that others will do the same.