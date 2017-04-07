---
title: Twitter's PWA is rubbish, but that's okay
date: 2017-04-07 00:00:00 Z
categories:
- '2017'
comments: true
image:
  feature: "../uploads/hero-twitter-pwa.png"
toc: true
excerpt: Twitter's Progressive Web App is finally out of testing, and it's not as
  good as the native app. Missing push notifications, wonky images, small text boxes,
  lack of sharing intents and confusing pull-to-update behaviour all highlight the
  challenge of building a PWA. The fact that Twitter is on-board with PWAs is a great
  step towards better web experiences for all.
layout: post
---

## The promise of PWAs

Progressive Web Apps bring a native-like application experience to websites. This is achieved through a combination of specifications like the web application manifest, service worker, web push API and (soon) webAPKs.

The advantages of using a website over a native application are numerous for consumers: faster install, more rapid updates and a significant reduction in the storage required. There are also advantages for application publishers: less friction to install (it's just a URL!), instant updates (no app store update process) and they are easier to develop for cross-platform audiences.

Normal websites can be upgraded to add great features such as a good offline experience and a more immersive browser view. This means that PWAs aren't just an alternative to native applications, it makes sense to roll these features out on websites anyway.

<br>

Have you ever started to install an application, then stop because it requested permission to record audio, spam all of your contacts, install a trojan horse or turn your phone pink? The web has a well developed permissions model for things like access to the camera, vibration, location and sensors. A PWA inherits all of this development in web permissions.

## Twitter

<figure align="center">
<img style="max-width:50%;" class="resp" data-width="50" data-src="https://webperf.ninja/uploads/twitter-app-size.png"/>
<figcaption>104MB of storage for the Twitter application</figcaption>
</figure>

Twitter's native application has over 500M downloads on the Google Play Store, and presumably a similar number on the App Store. Twitter has been experimenting with their mobile web experience over the past six months, adding PWA features to groups of users and measuring the response. On April 6 Twitter announced 'Twitter Lite', a fully-fledged progressive web app. The [marketing](https://blog.twitter.com/2017/introducing-twitter-lite) angle around the release is that it will improve the experience for users with low bandwidth mobile connections, especially those in Asia Pacific, Latin America and Africa.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Introducing Twitter Lite on mobile web! 📱<br><br>Loads quickly, takes up less space, and is data-friendly. Learn more: <a href="https://t.co/Zd825WOdQz">https://t.co/Zd825WOdQz</a> <a href="https://t.co/l1n0cYJuPc">pic.twitter.com/l1n0cYJuPc</a></p>&mdash; Twitter (@Twitter) <a href="https://twitter.com/Twitter/status/849866660882206721">April 6, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I jumped on the bandwagon, why would I want a massive native application, with frequent ~70MB updates, when the mobile website will give me the same experience?!

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Goodbye native app, hello fast web experience! <a href="https://t.co/xfQ3tY0hYW">pic.twitter.com/xfQ3tY0hYW</a></p>&mdash; Simon Hearne (@simonhearne) <a href="https://twitter.com/simonhearne/status/849970819258343424">April 6, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

> > I'm sad to say that I have now reverted to the native application, after less than 24 hours of using the PWA.

## Browser dependence

Before I discuss why I've gone back to the native application, it's worth discussing the inherent limitations of PWAs. The core PWA specifications of [service worker](http://caniuse.com/#feat=serviceworkers), [web app manifest](http://caniuse.com/#feat=web-app-manifest) and [web push](http://caniuse.com/#feat=push-api) are currently only supported on mobile devices running Android.

<figure align="center">
<img style="max-width:100%;" class="resp" data-width="100" data-src="https://webperf.ninja/uploads/caniuse-pwas.png"/>
<figcaption>PWA support</figcaption>
</figure>

This also means that the performance of the PWA is dependent on browser performance. Native applications can be optimised at a code-level to give the best performance, while PWAs have to rely on the browser to interpret the HTML, CSS and JavaScript provided. This may mean that PWAs perform more poorly than native applications.

## Things that just don't work

There are five key issues I have with the twitter PWA which have led me back to the native application, for now.

### 1) Text boxes are tiny, and broken

I use an increased font-size in my browser configuration, this is because so many websites use tiny font sizes and disable zooming on mobile. It's easier for me to just have bigger text everywhere. Unfortunately this breaks the way Twitter's input boxes grow with text, making it really awkward to edit or review a tweet.

<figure align="center">
<video autoplay muted loop poster="/uploads/text.jpg" style="width:80%; max-width:480px;">
  <source src="/uploads/text.webm" type="video/webm">
  <source src="/uploads/text.mp4" type="video/mp4">
</video>
<figcaption>Text boxes are too small and do not overflow correctly</figcaption>
</figure>

### 2) Push notifications are less reliable

I noticed a few times during my trial of the PWA that I would open Twitter to find unread notifications, but I had received no push notifications. On re-installing the native application I often get more notifications from the application than the PWA. The Web Push API depends on a [third-party server](https://developers.google.com/web/fundamentals/engage-and-retain/push-notifications/sending-messages) to send notifications, and it's generally fire-and-forget with no ability to re-send failed notifications.
Also frustrating is the lack of grouping of notifications, a popular tweet can quickly fill up your notifications!

<figure align="center">
<img style="max-width:60%;" class="resp" data-width="60" data-src="https://webperf.ninja/uploads/twitter-pwa-notifications.png"/>
<figcaption>Fewer notifications from the PWA</figcaption>
</figure>

### 3) Portrait images aren't re-oriented

When attempting to add a portrait picture, which the native application uploads with the correct orientation, the PWA has it sideways. This wouldn't be such an issue if the image could then be rotated in the PWA, but it cannot. As such this is a killer bug for me.

Another slight irritation is shown in the video below. There is no indication to the user that the image is being uploaded! This is on wifi and there is an eight second delay with no user feedback, while the whole browser is locked up. Considering that the PWA is designed for users with low bandwidth mobile connections, this delay could be significantly longer.

<figure align="center">
<video autoplay muted loop poster="/uploads/image.jpg" style="width:80%; max-width:480px;">
  <source src="/uploads/image.webm" type="video/webm">
  <source src="/uploads/image.mp4" type="video/mp4">
</video>
<figcaption>Images aren't correctly rotated, and there's no way to fix it</figcaption>
</figure>

### 4) Pull-to-...?

The native Twitter application has trained me to pull-to-update on the feed. Pulling down in other screens does nothing. Unfortunately, due to the dependence on the browser, this behaviour is not consistent in the PWA. It will reload the whole page if you pull on most pages. Implementing pull-to-update across the whole PWA might make this more consistent.

<figure align="center">
<video autoplay muted loop poster="/uploads/ptr.jpg" style="width:80%; max-width:480px;">
  <source src="/uploads/ptr.webm" type="video/webm">
  <source src="/uploads/ptr.mp4" type="video/mp4">
</video>
<figcaption>Pull-to-update behaviour is inconstistent.</figcaption>
</figure>

### 5) Sharing

One of the key features of the web is being able to share content. The native Twitter application adds sharing intents to menus, so that you can share content via tweets or direct messages from any other application (or browser) on your device. This is missing in the PWA which makes day-to-day use significantly more tricky - copy to clipboard, back to homescreen, open PWA, click the tweet button, tap-and-hold, paste text.


<figure align="center">
<img style="max-width:60%;" class="resp" data-width="60" data-src="https://webperf.ninja/uploads/twitter-share-fail.png"/>
<figcaption>Lack of integrated share options is frustrating.</figcaption>
</figure>

## Conclusion

So I've moved back to the native application. Of course that doesn't mean I can't use the PWA, as I can just open up [mobile.twitter.com](https://mobile.twitter.com/) and get the full PWA experience. The Twitter PWA is trying to do a lot, while browsers are still getting to grips with implementing the specifications. Having Twitter invested in the PWA ecosystem should really help to push the development along.

Committing to PWAs will continue to be a tough sell until Safari on iOS supports service worker, web push and web app manifests.