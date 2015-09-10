---
layout: post
title:  "Measuring Webpage Jank"
date:   2015-09-11 12:00:00
category: 2015
tags: [web, performance, webperf, jank]
comments: true
published: true
image:
  feature: "janky_hero.png"
---
#### Webpage jank can harm the user experience, here's an easy way to measure it on your pages

Here's the bookmarklet: 
<a style="cursor:alias;" class="btn btn-block" href='javascript:!function(e){function t(){for(var e=document.getElementsByClassName("fpser-lay"),t=e.length-1,n=t;n>=0;n--)try{document.body.removeChild(e[n])}catch(r){continue}var r=document.getElementById("fpser");r&&r.parentNode.removeChild(r)}function n(){if(t(),e.scrollTo(0,0),count=0,sh=Math.max(document.documentElement.clientHeight,e.innerHeight||0),h=Math.max(document.body.offsetHeight,document.body.scrollHeight)-sh,chunk=100,h-100<0)throw alert("I need to scroll, please reduce your browser height or choose a longer page!"),"Too short";fA=[],e.requestAnimationFrame(r),ll=!1}function r(){return ll?(e.scrollBy(0,chunk),tl=performance.now(),fA.push(parseInt(1e3/(tl-ll))),ll=tl,count+=chunk,void(count>=h?(e.scrollTo(0,0),a(fA)):e.requestAnimationFrame(r))):(ll=performance.now(),void e.requestAnimationFrame(r))}function o(e){var t=350,n=1,r=Math.max(parseInt(t/e.length-n),2),o="https://chart.googleapis.com/chart?chbh="+r+","+n+"&cht=bvs&chxt=y&chf=bg,s,00000000&chs=350x60&chm=D,FF0000,1,0,2,1&chd=t1:"+e.join(",")+"|"+Array(e.length).join("60,");return o.substr(0,o.length-1)}function a(e){var t=o(e),n=e.slice(0);e.sort(function(e,t){return e-t});var r=Math.floor(e.length/2);if(e.length%2)var a=e[r];else var a=(e[r-1]+e[r])/2;for(var l=e[0],i=e[e.length-1],c=0,s=0;s<e.length;s++)c+=e[s];var p=parseInt(c/e.length),d=document.createElement("div");d.id="fpser",d.style.cssText+=";font-family:sans-serif;font-weight:bold;width:400px;background:rgba(200,200,200,0.9);position:fixed;top:10px;right:10px;z-index:10002;padding:5px;box-shadow: 0px 0px 5px 2px rgba(0,0,0,0.75);text-align:center";var m=document.createElement("p");m.innerHTML="FPS: median = "+a+", mean = "+p+", min = "+l+", max = "+i,p2=document.createElement("p"),50>=a?(p2.style.color="red",p2.innerHTML="This page is JANKY (Framerate is below 50 FPS)"):a>=59?(p2.style.color="green",p2.innerHTML="This page is SMOOTH (Framerate around 60 FPS)"):(p2.style.color="yellow",p2.innerHTML="This page is ALMOST JANKY (Framerate above 50 FPS)"),p3=document.createElement("p"),p3.innerHTML="<a href=\"https://webperf.ninja/2015/jank-meter\">What is this?</a> | <a href=\"#\" onclick=\"window.FPS.cl();\">Hide this</a>";var s=document.createElement("img");s.src=t,d.appendChild(m),d.appendChild(s),d.appendChild(p2),d.appendChild(p3),document.body.appendChild(d);for(var u=0,s=sh;s<=h+sh;s+=100){var t=document.createElement("div");t.className="fpser-lay";var g="";if(g=parseInt(n[u])<50?"255,55,0":parseInt(n[u])<59?"255,255,0":parseInt(n[u])>0?"55,255,55":"55,55,55",t.style.cssText+=";border-bottom:1px solid black;line-height:"+chunk+"px;text-align:center;font-weight:bold;z-index:10001;position:absolute;width:80px;height:"+chunk+"px;left:0;top:"+s+"px;background:rgba("+g+",0.5);",parseInt(n[u])>0){var f=document.createElement("p");f.style.cssText+=";margin:0px",f.innerHTML=n[u]+" FPS",t.appendChild(f)}document.body.appendChild(t),u++}var t=document.createElement("div");t.className="fpser-lay",t.style.cssText+=";z-index:10001;position:absolute;width:80px;height:"+sh+"px;left:0;top:0;background:rgba(55,55,55,0.5);",document.body.appendChild(t)}n(),e.FPS={};e.FPS.cl=t}(window);'>Jank Meter</a>
 Drag it to your bookmarks bar or just add as a bookmark.

## What is jank?
Our eyes can't perceive visual changes at around 60 frames per second (FPS). As such, for smooth visual experiences most modern screens have a refresh rate of 60FPS. In order for our webpages to appear smooth to a user while interacting, all frames must render within 16ms (1000ms / 60 FPS). 

## What causes jank?
Anything that is expensive to process and causes the browser to repaint can cause jank. Common causes include large background images that move on scroll (parallax effect) and Javascript functions bound to scroll events. Paul Lewis ([@aerotwist](https://twitter.com/aerotwist)) wrote a [good post](http://calendar.perfplanet.com/2013/the-runtime-performance-checklist/) on some of the causes of jank back in 2013.

Here's an example of the jank meter on a web design agency's homepage. They use a jQuery plugin to create a parallax effect on large (but barely visible) background images.

<figure>
<img src="/images/janky_site2.png"/>
<figcaption>Jank Meter showing poor scroll performance</figcaption>
</figure>

Conversely, here's jankfree.org with a near-perfect scrolling experience:

<figure>
<img src="/images/jankfree_site2.png"/>
<figcaption>Jank Meter showing good scroll performance</figcaption>
</figure>

## How do you detect jank?
You can detect jank using the Timeline tab in Chrome Developer Tools. Simply hit the record button and scroll, then stop the recording and look for slow frames:

<figure align="center">
<img src="/images/devtools.png"/>
<figcaption>Dev Tools showing Jank</figcaption>
</figure>

You can also enable the framerate overlay in Chrome to show the live render performance:

<figure align="center">
<img src="/images/framerate.png"/>
<figcaption>Dev Tools showing FPS meter</figcaption>
</figure>

This can all be a bit time consuming though, recently I've found myself spending a lot of time in the timeline view just to detect jank.
The framerate meter also makes it difficult to identify exactly where in the page the jank is coming from.

I figured that there must be an easier way to do this. [requestAnimationFrame](http://www.paulirish.com/2011/requestanimationframe-for-smart-animating/) has been around for a few years now, it lets you make timer-based animations more efficient by synchronising reflow and repaint events.
This also gives us a clue as to how fast the browser can synchronise these events: ideally requestAnimationFrame should call your function every 16ms to get that silky-smooth 60FPS you want. If, however, it calls your function after 50ms you know that there has been something hogging the browser's time when it should have been repainting.
I created a small Javascript bookmarklet around this concept, scrolling down a page and measuring the effective framerate.

The bookmarklet produces a small overlay on the top-right of the screen showing the framerates achieved while scrolling the page. It also adds a bar to the left of the page showing what framerate was achieved for that scroll movement.

## Jank meter limitations
* Style is inherited, so it may look funny
* It depends on being able to scroll, so the page has to be longer than 2 x viewport height
* It relies on performance.now() and requestAnimationFrame() so it won't work in all browsers (latest Firefox and Chrome are fine)
* The chart image may not load on secure sites

There are probably a few more limitations, give it a go and let me know if you have any issues.
The code is in [a gist](https://gist.github.com/simonhearne/ef145e2732f2082771d3) so feel free to fork.

## How to fix jank?

Paul Lewis has a great [live demo](https://www.youtube.com/watch?v=QU1JAW5LRKU) on youtube of debugging and fixing jank in realtime.

There are a number of resources available, [jankfree.org](https://jankfree.org) is a great place to start.