---
title: 5 Web Performance Takeaways from Velocity Amsterdam 2016
date: 2016-11-08 13:08:00 Z
published: false
categories:
- '2016'
comments: true
image:
  feature: "../uploads/velocity_hillary_hero.jpg"
layout: post
---

Velocity Amsterdam has just come to a close. Here are the five key things that I am taking away from the two days of sessions.

## 1) Performance targets and KPIs are broken

This was one of the themes that ran like an undercurrent through the whole conference, starting with [Steve Souders](https://twitter.com/souders) at WebPerfDays talking about the death of window.onload for performance measurement. It's been known for a while that the onload event is flawed for measuring performance, but it has been universal across browsers so was the lowest friction number to get. The problem with measuring onload is that the number can be [gamed](http://www.leanblog.org/tag/gaming-the-numbers/) by moving content around and can be influenced by third-party content; onload does not necessarily bare any relation to user experience.

There are a great many alternatives to the onload event for measuring performance, from Speed Index to measure the speed of visual completeness to user timings to measure specific events on page loads. None of these are a silver bullet: Speed Index can be manipulated with skeleton content and is dependent on test speed and viewport size, user timings have to be carefully thought out and defined for specific page types, making them labour intensive.

[Denys Mishunov](https://twitter.com/mishunov) also spoke at WebPerfDays, he says that "recommendations and statistics are objective measures of performance, but user perception is not mathematics". Denys had some great examples of where objectively fast experiences had a poor user experience, such as a coin counting machine that users didn't trust because it [counted too quickly](http://www.90percentofeverything.com/2010/12/16/adding-delays-to-increase-perceived-value-does-it-work/). He extended this concept to the idea of passive- vs active-waiting: we can trick the user into thinking an interaction is just the right speed by manipulating the experience. [Optimistic UIs](https://www.smashingmagazine.com/2016/11/true-lies-of-optimistic-user-interfaces/) are an example of using this in the wild. This concept makes measuring simple timing points of pages almost totally irrelevant, instead we need to measure when the user thought that the event occurred, the delay until it actually occurred and the failure rate of the optimistic UI interaction.

One of the questions asked by the audience after [Kevin Bowman](https://twitter.com/__kb)'s great talk about [surviving big events](http://conferences.oreilly.com/velocity/devops-web-performance-eu/public/schedule/detail/53557) was 'what is the uptime SLA for Sky Betting'. Kevin's response was that they didn't have an official SLA, everyone just tries their best and they trust others to do the same. From my experience, having an SLA leads to gaming the numbers. This is especially true when there are incentives (i.e. a financial bonus) linked to the reported figure.

Gaming the numbers certainly is not restricted to web performance. The British National Health System has been highlighted as an organisation where KPIs have led to poor standards of care, leading to [unnecessary patient deaths](http://www.nationalhealthexecutive.com/Health-Care-News/nhs-performance-management-putting-standards-of-care-at-risk), even though the care givers give great concern to the welfare of their patients. KPIs are easy for senior stakeholders to set and measure - on paper they are the ideal way to get visibility into performance. Unfortunately static goals are open to abuse through manipulating the numbers in any number of ways.

To improve performance we should enable teams to be successful, to measure their own performance and set their own definitions of success.

## 2) Team success == business success
This was a positive theme that ran through a lot of the talks at velocity. We must enable our teams to do their jobs, let them make their own decisions and remove micro-management.
A great example of this was given by Kevin from Sky Betting. In the run up to the biggest event in SkyBet's calendar, they knew it was going to be tough. Kevin even said "we knew we were going to run out of compute resource, we just didn't know where". Team dynamics are critical in order to survive an event where just minutes of downtime can cost £100,000s of customer bets. SkyBet has cross-team 'squads', each of which has a responsibility on the production system. These squads are self-managing, so when something goes wrong they just get on and fix it. There were some close calls during the big event, with the platform almost coming to a stand-still. Kevin believes that the trust and independence of the squads allowed the issues to be resolved as quickly as possible, without large-scale war rooms which would have wasted valuable time.

## 3) We are under-utilising or abusing great Web features
HTTP/2 Push. Preload. PWAs

## 4) We still struggle with data visualisation

## 5) We need a performance conference

## BONUS - Corporate IT sucks

## SUPER BONUS - Empathise with your audience

