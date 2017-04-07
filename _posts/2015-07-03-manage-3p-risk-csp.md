---
title: Manage Third-party Risk Using a Content Security Policy
date: 2015-07-03 13:17:00 Z
categories:
- '2015'
tags:
- web
- performance
- webperf
- javascript
- third-party
- csp
- content-security-policy
- jquery
layout: post
comments: true
image:
  feature: csp_hero.png
excerpt: A feature to prevent cross-site-scripting may make it easier to police third-party
  javascript.
---

Andy Davies and I have [spoken](https://www.youtube.com/watch?v=9OtUOgx0cZg "What Are Third-party Components Doing to Your Site?") at a number of conferences about the risks that third-party components can have on your website.
In these talks we try to illustrate the fact that third-party components can have all sorts of negative consequences on your site's availability and performance.
At the end of our talks we are always asked the same thing: 'what can we do about it?'.

Once you've got your third-parties under control, set up a tag management solution and identified the business value you will still have some third-parties on your site.
What can we do to mitigate the risk that those critical third-parties pose?
There are a number of methods to minimise the risk, such as loading the third-party scripts with an [async or defer tag](https://www.youtube.com/watch?v=I5uhZcJ30SA "Guy Podjarny talks about Third-party Performance") (after ensuring that the third-party script [doesn't use document.write()](http://www.w3.org/TR/html401/interact/scripts.html#adef-defer "W3C Defer Specification")!).
The problem is that these third-party scripts can still make calls to fourth- and fifth- and sixth- ... parties, which can multiply the risk posed to your site.
We know this through using tools such as [request map](http://blog.webperf.ninja/portfolio/request-map/ "Request Map") which highlights how requests to these third-parties are made.

<figure style="float:right;">
<a href="http://requestmap.webperf.tools/render/150102_Q9_N37/">
<img src="/images/requestmap_very.png"/>
<figcaption>
Third-party calls can become complex and hard to manage
</figcaption>
</a>
</figure>

We don't currently have a good way to prevent these nth-party calls. Or at least not that people are using in the wild.
Content-Security-Policy is a proposed HTTP Header which prevents cross-site scripting (XSS) attacks. It does this by defining whitelists of domains which can load scripts, styles images etc. from.
This prevents resources being requested from malicious domains _at the client-side_.
CSP is [pretty widely supported](http://caniuse.com/#feat=contentsecuritypolicy "Can I use... CSP") amongst the major browsers and as it is just an HTTP header it can be set by any server-side language, any web server and any CDN.
Using your CDN would allow you to define geographic-specific third-party script whitelists which would be great to prevent calls to social networks from inside China, as an example.
I've built a quick example to demonstrate the concept [on my site](http://simonhearne.co.uk/sandbox/csp/ "Console message when unexpected third-party asset is blocked"):

<figure>
<a href="http://simonhearne.co.uk/sandbox/csp/">
<img src="/images/CSP.png"/>
<figcaption>Console message when unexpected third-party asset is blocked</figcaption>
</a>
</figure>

CSP will beacon back JSON every time a resource is blocked, it also has a [report-only feature](http://www.w3.org/TR/CSP/#content-security-policy-report-only-header-field "W3C CSP Report-only Mode"), where the request still happens at the client but it would allow you to report on unknown third-parties for further analysis.
A potential secondary benefit is that you can define the protocol in the CSP - thus enforcing HTTPS on the requests and better respecting your customers' privacy.

I can see a future where tag managers will integrate with CDNs (through [great APIs](https://docs.fastly.com/api/ "Fastly API Docs")) and will automatically create CSPs based on the tags that are loaded for each page and geography.
Wouldn't that be nice! Until then, though, it will take some manual intervention to get CSPs up-and-running.

Would you use this to restrict the third-parties on your site or is CSP too extreme for your needs? Please let me know if you try it out in the wild!