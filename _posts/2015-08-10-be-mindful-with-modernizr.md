---
layout: post
title:  "Be Mindful With Modernizr"
date:   2015-08-10 22:02:00
category: 2015
tags: [web, performance, webperf, modernizr, javascript, third-party]
description: "Modernizr might be making your site slow, especially on mobiles"
comments: true
published: true
image:
  feature: "parachute_hero.jpg"
  credit: flickr/jaguarcarsmena
  creditlink: https://www.flickr.com/photos/jaguarcarsmena/18769889306
---
#### Modernizr might be making your site slow, especially on mobiles

According to [Modernizr.com](http://www.modernizr.com/), Modernizr is a JavaScript library that detects HTML5 and CSS3 features in the user’s browser.
This framework tests for features in the user's browser then adds classes to your page declaring which HTML5 and CSS3 features are (and are not) supported in that browser.

Recently, a colleague was analysing a client’s site and noticed that performance on mobile was about one second slower than expected, with a gap in the WebPageTest waterfall with no network traffic.
We did some digging on desktop and could not replicate the one second of missing network time, although there was a clue hidden in the high CPU usage on the browser main thread, visible in the WebPageTest waterfall:

<figure style="text-align:center">
<a href="/images/waterfall_gap.png"><img style="box-shadow: 0 0 10px 0 rgba(0,0,0,0.75);padding: 10px;border-radius: 5px;max-width:80%" src="/images/waterfall_gap.png"/></a>
<figcaption>
High CPU usage and a gap in the waterfall at 6.5-7.5s
</figcaption>
</figure>

Something on the page was consuming the browser thread and blocking critical content including web fonts - meaning no text was rendered until this process had completed.
I decided to find more sites using Modernizr to see if the issue could be replicated - it could.

Take [www.CreativeBloq.com](http://www.creativebloq.com/) as an example. A Javascript bundle including Modernizr is loaded as object #6 on the homepage.
When loading it in a browser you can quickly see the browser thread being consumed by the Modernizr script in the Chrome Developer Tools Timeline:

<figure style="text-align:center">
<a href="/images/modernizr_desktop.png"><img style="box-shadow: 0 0 10px 0 rgba(0,0,0,0.75);padding: 10px;border-radius: 5px;max-width:80%" src="/images/modernizr_desktop.png"/></a>
<figcaption>
Over 150ms spent in modernizr.js - on a Core i7 processor
</figcaption>
</figure>

Note that the bulk of the time spent on this script is in one function - s.csstransforms3d. Following the stack you can see that this function causes a style recalculation.
A quick bit of digging into the Modernizr source identifies the cause. The script injects an element and then uses functions offsetLeft and offsetHeight to test whether a CSS 3D transform has worked on the enjected element:

{% highlight javascript %}
tests['csstransforms3d'] = function() {
    var ret = !!testPropsAll('perspective');
        if ( ret && 'webkitPerspective' in docElement.style ) {
            injectElementWithStyles('@media (transform-3d),(-webkit-transform-3d){#modernizr{left:9px;position:absolute;height:3px;}}',
	    function( node, rule ) {
		    ret = node.offsetLeft === 9 && node.offsetHeight === 3;
	    });
    }
    return ret;
};
{% endhighlight %}

This process makes sense - these offest function calls are a predictable way to test for the size of a DOM element on screen.
In order to calculate the size of the injected element these functions trigger a [reflow](https://developers.google.com/speed/articles/reflow?hl=en), in order for the browser to tell you the true size of an element it must ensure that all DOM manipulations (such as 3D transforms) have been executed.
Causing a reflow is generally considered bad for web performance, Stoyan Stefanov wrote a [great post](http://www.phpied.com/rendering-repaint-reflowrelayout-restyle/) on this way back in 2009.

Now, in order for Modernizr to do its thing properly it must load early. Here's what the [Modernizr documentation](http://modernizr.com/docs/) says:

> The reason we recommend placing Modernizr in the head is two-fold: the HTML5 Shiv (that enables HTML5 elements in IE) must execute before the <body>, and if you’re using any of the CSS classes that Modernizr adds, you’ll want to prevent a FOUC.

Ideally it should load before the other Javascript and CSS on the page to ensure that the correct features and styles are applied.
That means that the reflow behaviour is called twice - once for offsetLeft and once for offsetHeight - very early in the page load.
This is _bad_ for render performance, and it is _really bad_ on mobile where reflows (and the CSS 3D transform itself) are expensive in CPU time.

So, what do we do about it? First off, check if your Modernizr build runs the CSS 3D transforms check. If it does, make sure it is necessary and if not, remove it from your build using the Modernizr [production download tool](http://modernizr.com/download/).

Of course we need to make sure that we profile all of the Javascript on our sites, first-party and third-party.
We need to do this for every release, and every time a third-party changes.