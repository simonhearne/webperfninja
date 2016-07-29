---
title: Render Conf 2016 - Day 1
date: 2016-01-21 21:54:00 Z
categories:
- '2016'
tags:
- web performance
- render
- jquery
- conference
- '2016'
comments: true
image:
  feature: render_hero_bruce.jpg
layout: post
---

Render Conference - previously known as jQuery UK - was held in Oxford last week. It's a front-end conference for front-end people, which makes me a bit of an outsider. Performance is not the focus of Render Conference.

I rarely get to speak to front-end developers, the people who actually do the work. Render is an opportunity for me to hone up my front-end skills and get an idea of what front-end developers are up against and the latest technologies in play.

This post is a summary of the key talks from day one of Render Conference.

----------

### [Bruce Lawson](https://twitter.com/@brucel) - web.next

#### [Description](http://2016.render-conf.com/talks.php#webnext) | [Slides](https://speakerdeck.com/brucel/web-dot-next-render)

I had assumed that Bruce's talk would be identical to the [last few I've seen](/2015/velocity-europe-2015-report-1/#ensuring-a-high-performing-web-for-the-next-billion-people---bruce-lawson-opera-asa). Bruce's previous talks on web.next have focused on where customers are coming from and what devices they are using. This talk was much more focused around the web technologies that will *allow* the next 4 billion people to use the web.

Progressive Web Apps (PWAs) [will replace native mobile apps](http://loxima.com/blog/the-death-of-apps/) and this is a good thing: a relatively light-weight 20MB app might take over 30 minutes to install on 2G - by which time the network will probably have flaked out, Bruce notes.

PWAs increase accessibility to mobile users with limited devices and limited connectivity.

In telling his story, Bruce highlighted how browser manufacturers have had to collaborate to create better web technologies - and thus better user experiences. Mozilla, Google, Opera and Microsoft are trying to improve their relationship with web developers to produce scalable and useful functionality. AppCache is the counter-example Bruce uses to demonstrate what happens when this relationship is not built correctly.

Another great talk by Bruce, inspiring a room of front-end engineers to get involved with the Web Platform Incubator Group ([https://www.w3.org/blog/2015/07/wicg/](WICG)).

----------

### [Val Head](https://twitter.com/@vlh) - Designing Meaningful Animation

#### [Description](http://2016.render-conf.com/talks.php#designing-meaningful-animation)

Val believes that animation is often mis-used and mis-understood on the web. Throughout the talk Val uses a mocked-up registration confirmation form to demonstrate how animation can be used to reinforce a brand message.

Val references Disney's [12 basic principles of animation](https://en.wikipedia.org/wiki/12_basic_principles_of_animation) and highlights the key factors to focus on when animating on the web:

 * Staging
 * Follow Through
 * Timing
 * Secondary Action

Using a live example and the Chrome Developer Tools [animation controls](http://valhead.com/2015/01/06/quick-tip-chrome-animation-controls/) Val shows that animations can convey meaning and emotion when these four factors are considered properly.

----------

### [Alicia Sedlock](https://twitter.com/@aliciability) - The landscape of front-end testing

#### [Description](http://2016.render-conf.com/talks.php#the-landscape-of-front-end-testing) | [Slides](https://speakerdeck.com/aliciasedlock/the-landscape-of-front-end-testing)

Alicia knows that testing is hard, and that front-end developers aren't traditionally great at testing. By introducing testing framework language Alicia sets the scene for unit testing, introducing core concepts for front-end developers. The focus is on automation, making testing as simple as possible to drive adoption and engagement.

The testing concept then gets extended to visual regression testing, where Alicia lists the following automation tools to make this simple:

 * [PhantomCSS](https://github.com/Huddle/PhantomCSS)
 * [BackstopJS](https://github.com/garris/BackstopJS)
 * [Wraith](https://github.com/BBC-News/wraith)
 * [WebDriver.io](http://webdriver.io/)
 * [Percy.io](https://percy.io/)

Of course no talk on testing would be complete without a nod to accessibility. Alicia lists two tools to help with automating accessibility testing:

 * [a11y](https://github.com/addyosmani/a11y) / [grunt-a11y](https://github.com/lucalanca/grunt-a11y)
 * [pa11y](http://pa11y.org/)

And the final chapter in automated testing is performance (yay!). Alicia mentions a number of tools for automated testing:

 * [grunt-perfbudget](https://github.com/tkadlec/grunt-perfbudget)
 * [gulp-size](https://github.com/sindresorhus/gulp-size)
 * [perf.js](https://gist.github.com/tkadlec/7e352b74b1961a3e36d7)

I would add to the list a notable exception:

 * [SiteSpeed.io](https://www.sitespeed.io/)

----------

### [Harry Roberts](https://twitter.com/@csswizardry) - CSS for software engineers for CSS developers

#### [Description](http://2016.render-conf.com/talks.php#css-for-software-engineers-for-css-developers) | [Slides](https://speakerdeck.com/csswizardry/css-for-software-engineers-for-css-developers)

Harry starts his talk with a look back over his family history, highlighting that we have been use modern programming languages since 1959, the year his parents were born. CSS has only been around since 1996, but we have decades more software engineering experience which we can apply to CSS to make our projects more robust, scalable and predictable. I've noted down the core principles Harry advocates below:

 * Don't Repeat Yourself (DRY)
   * Your source should be DRY but the output can have repetition.
   * Use a preprocessor to store data in variables
   * Some repetition is better than a bad abstraction
 * Single Responsibility Principle
   * Use a class to denote a single responsibility, e.g. *class="button button-large button-positive"*
 * Separation of Concerns
   * Do not use CSS classes for JavaScript and vice versa
   * Do not bind CSS rules on to accessibility concerns, e.g. *role="navigation"*
   * Do not write CSS with JavaScript
 * Immutability
   * Do not allow any CSS rule to change, e.g. with a media query
   * Use responsive suffixes, as Harry defines in [BEMIT](http://csswizardry.com/2015/08/bemit-taking-the-bem-naming-convention-a-step-further/#responsive-suffixes)

I will never look at CSS the same. While a lot of this seems obvious when written down, how many times have you broken these simple rules?!

----------

### [Sara Soueidan](http://twitter.com/@SaraSoueidan) - SVG in motion

#### [Description](http://2016.render-conf.com/talks.php#svg-in-motion) | [Slides (PDF)](https://sarasoueidan.com/slides/SVG-In-Motion.pdf)

Sara is well-known as the SVG guru, in this talk she guides us through the perils and pitfalls of embedding SVG in our applications. It turns out that the way you embed an SVG image directly impacts what you can do with it. The table below summarises how you can animate SVG based on the way it is embedded, with the most flexible being an &lt;svg> element. This has the drawback of increasing your HTML size and reducing cache-ability, however.


| Embedding Technique | CSS Animations | JS Animations |
|---|---|---|
| &lt;img> | Inside &lt;svg> | N/A |
| url(); | Inside &lt;svg> | N/A |
| &lt;picture> | Inside &lt;svg> | N/A |
| &lt;iframe> | Inside &lt;svg> | Anywhere |
| &lt;object> | Inside &lt;svg> | Anywhere |
| &lt;svg> | Anywhere | Anywhere |  

Sara then details the various methods of animating SVG, with the following table summarising her recommendations:

| Animation | Technique |
|---|---|
| Transforms | JavaScript (or CSS) |
| Path Morphing | JavaScript |
| Line Drawing | JavaScript (or CSS) |
| Colour & Simple Animations | CSS (or JavaScript) |

The rest of Sara's talk goes in to detail on specific animations, path drawing and some cross-browser issues with transform-origin. Not to mention the fact that CSS transforms do not work in either Internet Explorer nor Microsoft Edge.

The part of Sara's talk I found most interesting was around manipulating the SVG viewbox property. By changing the value of the viewBox, you change the area of the canvas that is visible inside the SVG viewport. This enables you to zoom in to specific areas or objects. This can also enable you to manage SVG sprites and even step-animation in SVG.

----------

### [Robin Christopherson](http://twitter.com/@USA2DAY) - Technology – the power and the promise

#### [Description](http://2016.render-conf.com/talks.php#technology-the-power-and-the-promise)

Robin used a selection of videos and personal stories to remind us of how transformative the web is for people with disabilities. Even with the increased focus that developers put on accessibility, many web sites are totally inaccessible to blind people like Robin. New technologies such as automated intelligence, voice recognition and driver-less cars are all going to help people with disabilities, if only the designers and developers bear that in mind.

----------

### [Frederik Vanhoutte](http://twitter.com/@wblut) - Rendering the Obvious

#### [Description](http://2016.render-conf.com/talks.php#rendering-the-obvious)

Frederik started his talk with a reference to web performance - render the obvious. He mentions that we should show customers what they've got as soon as they've got it. From there the talk rapidly morphed into a psychedelic exploration of teaching and knowledge, using 'how a rainbow works' as a metaphor of a knowledge abstraction.

Children don't need to know exactly how a rainbow works, so a simple demonstration of a prism refracting light and creating the colours of the rainbow suffices. This is an abstraction away from how rainbows actually work, involving reflection and refraction in spheres of water. You can't hope to know everything, so accepting abstractions of knowledge in some areas is fine, but you must understand that everything you know is an abstraction...
