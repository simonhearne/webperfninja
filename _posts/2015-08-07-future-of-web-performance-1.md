---
layout: post
title:  "The Future of Web Performance - Part 1"
date:   2015-08-07 23:00:00
category: 2015
description: "Web performance is critically important, how will upcoming technologies change the way we manage it?"
tags: [web, performance, webperf, future]
comments: true
image:
  feature: "future_hero.jpg"
  credit: flickr/dunechaser
  creditlink: https://www.flickr.com/photos/dunechaser/9312170928/
---
#### Web performance is critically important, how will upcoming technologies change the way we manage it?

Web performance is [critical](/2015/web-performance-optimisation-basics/) to a successful online business.
Keeping on top of the latest technologies, techniques and practices allow us to stay ahead of the curve and get the edge over our competition.
This competitive edge comes through improved user experience and reduced operational costs (and the pride in achieving a [sub-1,000 Speed Index!](http://www.sitepoint.com/speed-index-measuring-page-load-time-different-way/))

New technologies are emerging which will change the face of web performance forever.
These technologies range from the underlying transport mechanism for our transmitted bytes to new javascript frameworks and an ever-growing range of browsing devices.
This complex and rapidly changing environment makes it harder than ever to plan and manage web performance.
In this short series I've attempted to summarise the key upcoming issues and describe how each one may impact your day-to-day life as a stakeholder in an online business.
I've also estimated when you need to really start thinking about it:

1. Now..
  *	[No Flash!](#noflash)
  *	[HTTPS Everywhere](#https)
  *	[Responsive Images](#responsive)
  *	[Mobile-First](#mobile)
  *	[Micro-Services and Containers](#micro)
2. Very Soon...
  * HTTP/2
  * _More_ Javascript?
  * Third-Party Functionality
  *	Emerging Markets
  *	Offline-First
3. Soon...
  *	ECMAScript 6
  *	Low-Powered Devices
  *	Social-First
  *	Rich Content
  *	Web 3.0 / Semantic Web

  
## <a name='noflash'></a>No Flash!

Flash has been around forever (well [10 years](https://en.wikipedia.org/wiki/Adobe_Flash#Macromedia) is forever in web-years).
It allowed web designers to create rich experiences and port them directly to the web in a format compatible with most operating systems and browsers.

_This. Was. Great._

So you want to embed a game on a page? Use Flash. So you want to have an interactive museum exhibit? Flash.
The uses were nearly endless, from poorly designed website introduction animations right through to online music albums.

The reason Flash was so universal is that you had the core code installed on your machine, the website element was just to tell the code where to download the Flash file from and how to render it.
This opens the client computer up to [quite](http://www.theguardian.com/technology/2015/jul/08/warning-adobe-flash-vulnerability-hacking-team-leak) a [few](http://blog.trendmicro.com/trendlabs-security-intelligence/analyzing-cve-2015-0311-flash-zero-day-vulnerability/) [security](http://www.computerweekly.com/news/4500248673/Adobe-patches-Flash-Player-vulnerability-CVE-2015-3113) risks.
Files from the web run directly in native code installed on your machine is generally a bad thing.

Flash is actually no longer available on mobile devices and has not been developed [since 2012](http://www.techhive.com/article/258574/adobe_says_no_flash_player_for_android_41_plans_to_withdraw_app_on_aug_15.html), making it pretty useless in a mobile-first world.
HTML5 offers us much more secure and flexible ways of rendering dynamic content, such as audio and video, on web pages.
CSS and Javascript offer the power to make even more interactive web experiences.
All of these together mean that Flash is dead.

Losing Flash is a positive change. Flash was [horrible for web performance](https://www.apple.com/hotnews/thoughts-on-flash/) and the modern replacements are more than up to the challenge.
The HTML5 and interactive client-side applications that replace Flash have their own performance challenges, however... (A story for another blog post or ten).  


## <a name='https'></a>HTTPS Everywhere

The Electronic Frontier Foundation created a browser plugin called [HTTPS Everywhere](https://www.eff.org/Https-everywhere) in 2011 and it has been in active development [since 2012](https://github.com/EFForg/https-everywhere/graphs/contributors).
The plugin will always try to redirect to a secure version of a site and its third-party resources. The intention of the plugin is to increase the security of your connections and to keep your data [private across the network](http://mashable.com/2011/05/31/https-web-security/ "Web Security: Why You Should Always Use HTTPS").
Google Chrome is planning to mark non-HTTPS pages as [affirmatively non-secure in the future](https://www.chromium.org/Home/chromium-security/marking-http-as-non-secure).
This means that, as a site owner, you should expect all traffic to be served securely over HTTPS (oh, and you must [use TLS not SSL](https://tools.ietf.org/html/rfc7568)).
This paradigm shift has significant performance implications as secure connections take time to establish.
To optimise secure connections ensure that HTTP keep-alive is enabled (the default for HTTP/1.1), that you have [session ticketing](http://chimera.labs.oreilly.com/books/1230000000545/ch04.html#_session_tickets) enabled and that your negotiating server is optimised for rapid negotiation.
Ilya Grigorik runs the site [isTLSfastyet.com](https://istlsfastyet.com/) which has much more information on the topic (hint: the answer is yes, TLS is fast when done right!).


## <a name='responsive'></a>Responsive Images

Delivering content to multiple device-types *well* is _hard_.

Delivering content to mutliple device-types *fast* is _really hard_.

We all know that [desktop is dying](http://qz.com/393553/the-desktop-is-dying-and-mobile-is-winning-in-news-like-everything-else/), giving way to mobile and tablet consumers ([especially while commuting](http://internetretailing.net/2015/07/consumers-to-spend-9-3bn-shopping-on-mobile-while-they-commute-study-finds/ "Consumers to spend £9.3bn shopping on mobile while they commute")).
As images make up [over 50%](http://httparchive.org/interesting.php#bytesperpage) of the average site, and bandwidth is limited with mobile connectivity, delivering a fast responsive site to all users means sending the smallest images possible whilst maintaining visual quality.

This is by no means an easy task, otherwise companies would not be [selling services](https://www.resrc.it/) specifically to make it easier.
Fortunately for us, new HTML specifications are [being drawn up](http://responsiveimages.org/ Responsive Image Working Group) and [implemented in browsers](http://caniuse.com/#feat=srcset "CanIUse.com / SrcSet") which will help in our quest.
These new specifications allow us to define images with breakpoints, just [like our CSS](https://css-tricks.com/css-media-queries/), so that smaller devices get the correct size images and retina displays get their high resolution versions.
See the [srcset definition](http://www.w3.org/html/wg/drafts/html/master/semantics.html#attr-img-srcset) for a good place to start, and a useful explanation on [CSS-tricks](https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/).

Unfortunately for us, this creates more work in creating the multiple image versions on top of the additional markup required in our HTML.

Hey, I didn't say we were getting a free ride.

Some build and automation tools will make this process easier for you, however. See the [Grunt Responsive Images](https://github.com/andismith/grunt-responsive-images) plugin (thanks to [Andi Smith](https://twitter.com/andismith "Andi Smith on Twitter") as an example of responsive image automation.

If this all seems a bit much, your CDN or content delivery provider may be able to do it for you with little work on your end. Whatever happens, we need to keep marketing happy by delivering the best quality images, keep development happy by automating everything and keep IT happy by minimising cost of delivery.

This is not a small task!


## <a name='mobile'></a>Mobile-First

I've mentioned earlier in this post that consumers are moving towards mobile devices.
This shift in consumer behaviour is also causing a shift in the way we build our websites.

Mobile-first means developing your site to work on mobile devices, then scaling the design up to larger screens.
This is as opposed to traditional responsive design which tends to wrangle desktop sites into smaller form-factors.

Being mobile-first means opening up your potential audience to the next _billion_ online consumers.
This point was made extremely well by [Bruce Lawson](https://twitter.com/brucel "Bruce Lawson on Twitter") in [his keynote](https://www.youtube.com/watch?v=BHO70H9tvqo) at Velocity Santa Clara 2015.
Potential consumers in under-privileged areas *will* access your web site or application using a mobile device. Period.

Beyond the obvious advantages in being mobile-friendly, all types of online business will have customers following links from social media on their mobile phones.
Unfortunately, these types of clicks generally use the webview built in to the social application rather than a 'proper' web browser.
This means that there are even more platform / device / browser combinations to worry about and further considerations on web performance (which cache will I use? What resources will I get?).

Designing for mobile-first means layouts that start small and grow with the screen, minimal network interactions and use of key HTML5 features such as [Open Graph](http://ogp.me/).

Designing for _fast_ mobile-first means:

*   Heavy use of caching
*   Optimal use of network time
*   Removing _all_ unnecessary third-party assets
*   Removing (or at least profiling) Javascript - no event handlers on touch or scroll please!
*   Fitting first-render into one round-trip - that means critical CSS is inline, with cacheable CSS added with Javascript


## <a name='micro'></a>Microservices and Containers

Containers and Microservices are real buzz-words at the moment.
If you are unfamiliar with the terms have quick read of [this Medium article](https://medium.com/aws-activate-startup-blog/using-containers-to-build-a-microservices-architecture-6e1b8bacb7d1) on the topic.

Breaking a monolithic application into atomic components - each with their own function and service definition - is a very logical move.
Microservices have many benefits:

*   Rapid development cycles - rapidly iterate services on fixed service definitions
*   Easy replacement of functionality - changing payment provider? Replace the payment service
*   Simple testing during development - stubbing of services means that each can be tested for performance and functionality in isolation
*   Logical scalability - scale each component as necessary rather than the whole application

There's no escaping microservices. The concept offers many benefits and will apparently make web application development much more simple.

There are various performance and security issues that we need to be aware of though. 
I won't try to enumerate all of the potential issues that microservices create - because [Gareth Rushgrove](https://twitter.com/garethr "Gareth Rushgrove on Twitter") did it better than I could ever do at the most recent [London Web Performance Meetup](http://www.meetup.com/London-Web-Performance-Group/).
Please find his fantastic slides [here](https://speakerdeck.com/garethr/containers-and-microservices-make-performance-worse).

Wow, that's quite a list of things we need to care about, and I haven't even started to consider the way we measure and monitor site performance.
Using [WebPageTest](https://webpagetest.org/), [sitespeed.io](http://www.sitespeed.io/), [SpeedCurve](https://speedcurve.com/) or similar to test front-end performance before any release is _critical_.
We also need to ensure that we include mobile and responsive breakpoint testing.
