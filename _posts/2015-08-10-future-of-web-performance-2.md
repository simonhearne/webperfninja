---
title: The Future of Web Performance - Part 1
date: 2015-08-10 13:17:00 Z
published: false
categories:
- '2015'
tags:
- web
- performance
- webperf
- future
layout: post
comments: true
image:
  feature: question_hero.jpg
  credit: flickr/eleaf
  creditlink: https://www.flickr.com/photos/eleaf/2536358399
---

#### Web performance is a hot topic now, how will upcoming technologies change the way we manage it in the future?

Web performance is critical to a successful online business. Keeping on top of the latest technologies, techniques and practices allow companies and individuals to stay ahead of the curve and get the edge over competitors. This comes through improved user experience and reduced operational costs. New technologies are emerging which will change the way we manage web performance forever. These technologies range from the underlying transport mechanism for our bytes to new javascript frameworks and an ever-growing range of web-browsing devices. This complex and rapidly changing environment makes it harder than ever to plan and manage web performance. In this series I've attempted to summarise the key upcoming issues and describe how each one may impact your day-to-day life as a stakeholder in an online business. I've also estimated the time where you need to really start thinking about it. This post covers the issues that you should be considering now, further posts cover:

*   In the next 6 months
*   Beyond 6 months

So without further adieu, technology changes affecting web performance _now_:

*   No Flash!
*   HTTPS Everywhere
*   Mobile-first
*   Responsive Images

## No Flash!

Flash has been around forever (well [10 years](https://en.wikipedia.org/wiki/Adobe_Flash#Macromedia) is forever in web-years). It allowed web designers to create rich experiences and port them directly to the web in a format compatible with most operating systems and browsers. This. Was. Great. Want to embed a game on a page? Use Flash. Want to have an interactive museum exhibit? Flash. The uses were nearly endless, from poorly designed website introduction animations right through to full online music albums. The reason Flash was so universal is that you had the core code installed on your machine, the website element was just to tell the code where to download the Flash file from and how to render it. This opens us up to [quite](http://www.theguardian.com/technology/2015/jul/08/warning-adobe-flash-vulnerability-hacking-team-leak) a [few](http://blog.trendmicro.com/trendlabs-security-intelligence/analyzing-cve-2015-0311-flash-zero-day-vulnerability/) [security](http://www.computerweekly.com/news/4500248673/Adobe-patches-Flash-Player-vulnerability-CVE-2015-3113) implications, files from the web run directly in native code installed on your machine. Flash is actually not available on mobile devices and has not been developed [since 2012](http://www.techhive.com/article/258574/adobe_says_no_flash_player_for_android_41_plans_to_withdraw_app_on_aug_15.html) making it pretty useless in a responsive world. HTML5 offers us much better, more secure and more flexible ways of rendering dynamic content such as audio and video. CSS and Javascript offer the power to make interactive web experiences. All of these together mean that Flash is dead. Which is great because it was horrible for web performance. The HTML5 and interactive client-side applications that replace Flash have their own performance challenges however.  

## HTTPS Everywhere

The Electronic Frontier Foundation created a browser plugin called [HTTPS Everywhere](https://www.eff.org/Https-everywhere) in 2011 and it has been in active development [since 2012](https://github.com/EFForg/https-everywhere/graphs/contributors). The plugin will always try to redirect to an HTTPS version of a site and of third-party resources, thus increasing the security of your connections and keeping your data private across the network. Google Chrome is planning to mark non-HTTPS pages as [affirmatively non-secure in the future](https://www.chromium.org/Home/chromium-security/marking-http-as-non-secure). This means that, as a site owner, you should expect all traffic to be served over HTTPS (oh, and you must [use TLS not SSL](https://tools.ietf.org/html/rfc7568)). This has performance implications as TLS connections take time to establish, and your customers likely need to make much more than one connection! To optimise secure connections ensure that HTTP keep-alive is enabled (the default for HTTP/1.1) and that your negotitiating server is opimised for rapid TLS negotiation. Ilya Grigorik runs the site [IsTLSFastYet](https://istlsfastyet.com/) which has much more information on the topic (hint: the answer is yes!).

## Responsive Images

Delivering content to multiple device-types well is _hard_. Delivering content to mutliple device-types fast is _really hard_. We all know that [desktop is dying](http://qz.com/393553/the-desktop-is-dying-and-mobile-is-winning-in-news-like-everything-else/), giving way to mobile and tablet consumers. As images make up [over 50%](http://httparchive.org/interesting.php#bytesperpage) of the average site, and bandwidth is limited with mobile connectivity, delivering a fast responsive site to all users means sending the smallest images possible whilst maintaining visual quality. This is by no means an easy task, otherwise companies would not be [selling services](https://www.resrc.it/) specifically for it! Fortunately for us, new HTML specifications are [being drawn up](http://responsiveimages.org/) and [implemented in browsers](http://caniuse.com/#feat=srcset) which will help. These allow us to define images with breakpoints, just like our CSS, so that smaller devices get smaller images and retina displays get their 2x resolution versions. See the [srcset definition](http://www.w3.org/html/wg/drafts/html/master/semantics.html#attr-img-srcset) for a good place to start, and a useful explanation on [CSS-tricks](https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/). Unfortunately for us, this means more work in creating the image versions and the additional mark-up required in our HTML. Hey, I didn't say we were getting a free ride. Some build and automation tools will make this much easier for you, however, such as the [Grunt Responsive Images](https://github.com/andismith/grunt-responsive-images) plugin (thanks to Andi Smith). If this all seems a bit much, your CDN or content delivery provider may be able to do it for you with little-to-no work on your end.  

## Mobile-First

I've just mentioned the move from consumers on desktop machines to consumers on mobile devices when discussing images. This shift in consumer behaviour is also causing a shift in the way we build our websites. Mobile-first means developing your site to work on mobile devices then scale up to larger screens, as opposed to traditional responsive design which wrangles desktop sites into smaller form-factors. It also means opening up your potential market to the next _billion_ online consumers as put extremely well by Bruce Lawson in [his keynote](https://www.youtube.com/watch?v=BHO70H9tvqo) at Velocity Santa Clara 2015. Beyond the obvious advantages in being mobile-friendly, all types of online business will have customers following links from social media on their mobile phones, generally using webviews rather than a 'proper' web browser. So there are even more device / browser combinations to worry about! Designing for mobile-first means layouts that start small and grow as well as minimal network interactions. Designing for _fast_ mobile-first means:

*   Heavy use of caching
*   Optimal use of network time
*   Removing third-parties
*   Profiling Javascript (no eventhandlers on touch or scroll please!)
*   Fitting first-render into one round-trip

## Third-Party Javascript

It's no surprise that most websites are using more third-party Javascript. There can be huge value in services that provide analytics, insight, remarketing, a/b testing, comments, imagery, etc... The problem is, we're not good at managing the performance impact of these third-parties. Issues can range from an A/B testing script making the add to basket button unusable to simply increasing the page load time. What compounds the problem of third-party javascript is that it is almost always added to the site in live, after performance testing has happened. Even if you test third-parties on your live site, they will be on a different release schedule to you. As these scripts are loaded from the third-party domain you generally have no control over the code that is executed which, beyond the security implications, can make it very hard to manage the impact they have on your site's performance. Unfortunately, this is not a problem we can solve easily. The only way to measure the impact of third-parties on your site is with a Real User Monitoring solution which collects data on your third-party requests. Critically, the third-party needs to have the Timing-Allow-Origin header to get detailied performance data (Andy Davies wrote [a good post](http://calendar.perfplanet.com/2012/an-introduction-to-the-resource-timing-api/) about this in 2012!) Beyond measuring the performance of third-parties, being able to rapidly remove them from your site and keeping a close eye on the site after code releases are key.  

## HTTP/2

If HTTPS Everywhere seems scary, how about a whole new protocol which will only run over secure connections? Well, that's HTTP/2. The current version of the session layer used for the web is HTTP/1.1, this standard was proposed in 1996 and has never actually been ratified! For over half of the history of the World Wide Web we have been using the same hacky protocol. HTTP/2 was designed for the modern web (i.e. pages with more than one asset and multiple mime-types), thus it will change the very fabric of web performance. HTTP/2 uses one connection per host to send all of the necessary assets, with fun concepts such as multiplexing and parellelisation. It also adds shared-dictionary compression of content AND headers as well as the ability for servers to push content to browsers. This is a pretty huge paradigm shift The key thing to keep in mind is that most of our well-known performance optimisations were effectively hacks around the inefficiencies of HTTP/1.1:

*   Combining files - Javascript, CSS, Image Sprites can (and should) all be split back out to their component files over HTTP/2 for better prioritisation and caching
*   Domain Sharding - each shard will require a new TLS negotiation incurring additional time cost and will offer little or no benefit
*   DataURIs / Encoded images - should be moved back to individual files for better prioritisation and caching

There are multiple posts on the web detailing the changes to web performance that will come with HTTP/2, I've listed a few of the best ones below. Generally, HTTP/2 will _improve_ the performance of the web, although sites that have not optimised well for HTTP/1.1 may get the most benefit! ECMAScript 6 Emerging Markets Offline First Low-Powered Devices Social-First Rich Content Web 3.0 / Semantic Web