---
layout: post
title:  "Questions to Ask Your Third-Parties"
date:   2015-07-03 13:17:00
category: 2015
tags: [web performance webperf javascript third-party]
comments: true
---
## We need rules to keep third-party Javascript in check.

We've discussed how to [find the third-party assets](http://webperf.ninja/2015/find-third-party-assets/) on your site and started to look at how to [mitigate the risk](http://webperf.ninja/2015/manage-3p-risk-csp/) that they pose.
But what should you do when you add new third-parties to the site?

There are some key questions you need to ask of the third-parties to ensure that they will not impact the user experience, performance or security of your customers.
In the best-case scenario you have the opportunity to ask these questions before signing a contract with the third-party in question.
In the more common case, someone else has already created a relationship and has just requested that the tag be added to your site.
Either way, having a list of questions to ask will give you an idea of how mature the third-party is and how much work will be required to ensure that your customers continue to have a great experience.

[JSManners.com](http://jsmanners.com/) by [@triblondon](https://twitter.com/triblondon) was designed to address exactly this issue, giving a list of questions that you can ask a third-party to give them a score.
I'm a fan of scores, they're simple and easy to report on. For assessing third-parties, though, there are more qualitative assessments to make.
For example you may not be willing to use a third-party which includes jQuery outside of a protected scope (as the risk of breaking your site is too high) but you are willing to accept 1kB of cookie data on your host domain.
So I've borrowed the list of questions from JSManners and re-organised them into categories, I've also removed some and added others as well as adding some context to each point so that you can understand the reasoning for the question.

* **Critical Questions**

	*   Are common 3rd party libraries (e.g. jQuery, Underscore, Backbone) included outside of a protected scope (ie is there any chance they may conflict with other instances of the same library that may be included on the page? _- If common libraries conflict, it may break critical functionality of your site. Third-parties are on different release cycles to you so even if everything works now, it may not in the future._
	*   Do component script(s) block render in any way? _- If a third-party asset blocks the render of your page(s), it is a single-point-of-failure (SPOF). Thus if your customers cannot download their script for any reason, it will take [at least 20 seconds](http://www.stevesouders.com/blog/2014/11/14/request-timeout/) to render your page(s). You want to  know about this and mitigate the risk (by asking all of the availability questions below!)_
	*   Do component script(s) use document.write? _- if so, you cannot load them asynchronously, every DOM element below the inserted script is [blocked from rendering](http://www.stevesouders.com/blog/2012/04/10/dont-docwrite-scripts/) while it downloads and it [blocks other dynamic scripts](http://www.stevesouders.com/blog/2012/04/10/dont-docwrite-scripts/)._  

	<br/>
* **Good Behaviour**

	*   How many objects/variables do component script(s) require in / add to the global scope?
	*   Do component script(s) produce any console output in normal operation? _- they shouldn't; if they do, why and what content is output?_
	*   Do component script(s) cause any JavaScript errors in normal operation? _- they shouldn't; if they do, why and what content is output?_
	*   Can component script(s) be loaded asynchronously? _- ideally scripts should be loaded asynchronously to prevent potential impact on your [users' experience](https://css-tricks.com/thinking-async/)._
	*   How many (infinitely and unconditionally recurring) timer events does the script fire per minute? _- timer events such as setInterval() can cause the main browser thread to lock up in some circumstances and can cause performance issues if the functions access the DOM or perform network actions._
	*   If the script tag is removed from the page (e.g. because it appears to be causing problems), what is the UI impact (on subsequent page loads)? _- if you have a method of removing badly-behaving scripts, you should ensure that the customer experience is not negatively impacted. This may be relevant for a third-party that adds content to the page such as adverts or personalisation._
	*   Which browsers is the component script tested in? _- if the third-party can't guarantee that the script will behave well in all of the browsers you support then you can't guarantee your user experience._
	*   When does the script interact with the DOM? _- if the script interacts with the DOM on regular, critical or unpredictable events there may be a significant performance impact._
		*   On parse
		*   On the DOMReady event
		*   On the load event
		*   On recurring timer events
		*   On user interaction events
		*   On network related events
		*   When invoked by a function call on JS API

	<br/>
* **Local Storage**

	*   Does the script set any persistent cookies on the host domain? _- this may be bad, I've seen a customer site which sends 200kB of upstream cookie data on each page load because of third-party cookies set on the host domain._
	*   Does the component depend on, or modify, any existing cookies set by the host page? _- it shouldn't, these are your cookies._
	*   What is the maximum total size of data, in bytes, stored in cookies by the script? _- depending on the domain, a large amount of upstream cookies can cause performance issues. Remember that cookies cannot be compressed on the network (at least with HTTP/1.1)._
	*   Does the component persist data in the browser using a mechanism other than cookies? _- you should be aware if the third-party relies on localstorage or equivalent and ensure that there are no security or performance risks associated with it._

	<br/>
* **DOM Interaction**

	*   If the component adds event listeners to DOM elements, does it remove them when they're no longer required?

	<br/>
* **Content Delivery**

	*   Is the script (including all non-dynamic resources) cached on a CDN with global reach? _- using a CDN ensures that the resources are delivered to your customers as quickly as possible and shows that the third-party understands the importance of performance._
	*   Where are there servers that can accept write operations performed by the script? _- if the browser needs to send data back to the third-party, having locations close to your customers ensures best possible performance and that data won't be lost due to poor connections._
	*   What is the total data size in kilobytes transferred on page load? _- large amounts of Javascript can cause performance issues, ensuring that the third-party only delivers necessary content._
	*   What is the minimum browser-cache TTL (in seconds) of files downloaded when the component script loads (ie. Cache-control max-age)? _- having good cache control on third-party assets reduces the amount of network time for repeat visits, however some third-parties will disable all caching as the scripts are dynamic._

	<br/>
* **Analytics**

	*   Do the component script and all associated resources provide ResourceTiming [opt-in header](http://www.w3.org/TR/resource-timing/#cross-origin-resources) (ie. [Timing-Allow-Origin](https://nccgroup.webex.com/mw0401lsp13/mywebex/default.do?service=1&siteurl=nccgroup&nomenu=true&main_url=%2Fmc0901lsp13%2Fe.do%3Fsiteurl%3Dnccgroup%26AT%3DMI%26EventID%3D349336237%26UID%3D504506122%26Host%3DQUhTSwAAAAJ8Y2XjDvwHvaWR52DTDaT-zR08KLPczSY835Z46AfLT52IErW9zlPt5lkk-nSo-xT6NY8Q5oCfFw2U0-39b8pJ0%26FrameSet%3D2%26MTID%3Dm4dad1c514e54409238c2142cd843ae2d): *)? _- if you are using a real user monitoring (RUM) solution, this header allows you to measure and record detailed timings of your third-party resources. There may be security implications here though._

	<br/>
* **Availability**

	*   Is the script or any web service it depends on served from a single origin (ie. is there just one origin data center)? _- this could be a single-point-of-failure for the third-party._
	*   In the event of a complete failure of the primary origin (eg unmitigated data centre power failure), what is the mean time to recovery (MTTR), in seconds? _- this checks that the third-party are aware of the consequences of the origin becoming available._
	*   How many full outages has the service experienced in the 12 months prior to today? (where full outage means a user with empty cache anywhere in the world being unable to use the service) _- this gives you an idea of how reliable the service will be. Based on the impact of the service being unavailable this could be a deal-breaker._
	*   Is there a public status page describing the current operational state of the script's backing services? _- if the third-party is open about uptime and performance this serves as a good indicator of their maturity._

	<br/>
* **Transport**

	*   What is the minimum number of HTTP requests that the script will make when invoked? _- if this number is high it suggests an inefficient design, creating more network traffic than is ideal._
	*   Is it possible to make ALL the script's network activity go over HTTPS? _- your customers trust you with their information, third-parties become potential leaks of this information and HTTPS helps to reduce the risk._
	*   Is HTTP 2.0 supported for all requests? _- HTTP 2.0 is the newest HTTP protocol which enables more efficient communications. In most browsers it is only enabled over HTTPS._
	*   Can the script's initial payload be bundled with the host page's own scripts? _- this reduces the network overhead and delay of the initial request. It can also mitigate the risk of the third-party being unavailable and keeps the core code under your control, meaning that you manage the new third-party code releases to your site._

	<br/>
* **Security**

	*   Will the component be involved with collecting user identifiable data (including any one of name, email address, credit card details, or phone number)? _- any of this can be risky and may be against the law in some of your customers' countries or open you up to PCI compliance issues._
	*   For European customers, does the script's backing service either a) not store any personal data, b) store personal data only within the EU, or c) store personal data outside the EU in compliance with the US Safe Harbour data protection standard? _- you should ensure that your third-parties are not putting your customers' data at risk, pursuant to your (and your customers') local and international laws._
	*   Does the script respect the Do-Not-Track HTTP header, either actively or by not conducting any tracking at all? _- Do-Not-Track is a [proposed HTTP header](https://en.wikipedia.org/wiki/Do_Not_Track) which suggests that customers can opt-out of cross-site behaviour tracking. If your third-party respects the DNT header then they have respect for your customers' privacy wishes._