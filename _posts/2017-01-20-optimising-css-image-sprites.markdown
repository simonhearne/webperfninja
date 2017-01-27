---
title: How to Optimise CSS Image Sprites
date: 2017-01-20 00:00:00 Z
categories:
- '2017'
comments: true
image:
  feature: "../uploads/hero-sprite.png"
toc: true
layout: post
description: Optimising sprites might be more important than you think, and easier than you expect!
---

CSS image sprites can provide a performance benefit for most sites.
A sprite combines multiple small images into one file and CSS slices out the relevant sections of the image when they are required.
This reduces the number of requests required to render a page, potentially meaning that the page renders faster over HTTP/1.1.

The humble sprite can become critical to web performance. It is common to see the main website logo buried in the middle of image slider controls and social media icons.
Unfortunately, like all images, sprites can become bloated and slow.

Here are some top tips to improve your sprite's performance:

## Remove your logo image

Serve your logo image as a separate file, referenced in an ```<img>``` element.
This will be downloaded earlier than the sprite file (which is discovered late by the browser).
<figure align="center">
<img style="max-width:50%;" src="/uploads/amazon-sprite.png" />
<figcaption>Amazon used to put its logo in a sprite. Why?!</figcaption>
</figure>

A secondary benefit is that the logo asset can be cached for a very long period, 
unaffected by minor changes to the other icons in the sprite.

## Remove icons that are available in UTF-8

It's common to see simple elements such as left and right arrows included in sprites.
Oftentimes there is a UTF-8 symbol which provides a suitable match. <a href="https://www.utf8icons.com/">UTF-8 Icons</a> provides a good reference.
<figure align="center">
<img style="max-width:50%;" src="/uploads/utf8-icons.png" />
<figcaption>Some of the characters available for free in UTF-8</figcaption>
</figure>

## Use CSS filters

Want to change the colour of an icon when someone hovers over it? Don't add another image to the sprite, use CSS filters to do it automatically.
A ```:hover``` rule like ```filter:hue-rotate(90deg);``` or ```filter:invert(100%);``` might just do the job!

## Separate icons with very different colours

PNG compression works best for a limited colour palette. If your sprite has images with complex colours, consider moving them to a separate image.
A good test of this is to save your image as a PNG8 and see if any of the colours are lost in the process.

## Save as a PNG8

Most image editors will save PNG files that have transparency as PNG32 by default.
This allows for 24 bits of colour data (true colour = >16.7 million colours) as well as 256 levels of transparency.

PNG8 allows for 255 colours plus on/off transparency. This should be plenty for most sprites and significantly reduces file size.

<a href="https://tinypng.com/">TinyPNG.com</a> is a good place to start optimising your sprite.

## Remove whitespace

Whitespace is totally unnecessary in a sprite, as the CSS is defined at a pixel level.
While extra whitespace will not have a significant impact on filesize, thanks to PNG compression, the memory footprint on the device will be increased.
In a world of £50 Android phones from Amazon, we have to be extremely conservative with memory usage.

<figure align="center">
<img style="max-width:50%;" src="/uploads/sprite-whitespace.png" />
<figcaption>That's a lot of wasted memory</figcaption>
</figure>

## Make it square

This may be a micro-optimisation, but square images are more efficient than rectangles on memory-constrained devices.