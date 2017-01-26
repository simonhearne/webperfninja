---
title: Content Security Policy - the surprising site speed win
date: 2017-01-26 20:26:00 Z
published: false
---

I'm working on a new version of [requestmap](https://requestmap.webperf.tools). Instead of plotting the domains on a site, the [new requestmap](https://requestmap.herokuapp.com) plots every. single. request. As you might imagine this can get messy, I'm still working on how best to represent such a large number of data points.

For now, this new version works well on relatively simple websites. Such as this blog. The number of requests to load this page should be under ten: an HTML document, a CSS bundle and a few images. No JavaScript, well except for Google Analytics. Oh, and Disqus. 

I use Disqus for comments as this site is hosted on GitHub, there is no server-side environment to manage comments myself. Besides, why have a database and server-side code when a third-party will do it for free?

The requestmap below shows every request Chrome makes when loading a blog post on my site. The area highlighted in green is content that *I* am in control of. The rest? That's Disqus.

<figure align="center">
<a href="https://requestmap.herokuapp.com/render/170126_3F_KXC">
<img style="max-width:80%;" src="/uploads/ninja_requests.png"/>
<figcaption>Content I've added to my site in green, everything else is from Disqus.</figcaption>
</a>
</figure>

I found this out by chance, while testing requestmap. When I first added Disqus comments there were *no* unexpected requests. I'm not sure what's changed, but I assume that this is how Disqus monetises their free service.

Beyond the number of third-party requests that I was subjecting my visitors to, the impact on CPU was pretty huge. 