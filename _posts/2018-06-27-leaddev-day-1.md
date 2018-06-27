---
title: Lead Developer Conference (London) - Day 1!
date: 2018-06-27 00:00:00 Z
categories:
- '2018'
comments: true
toc: true
image:
  feature: "../images/leaddev_hero.jpg"
excerpt: Lead Developer is a conference for senior and lead software engineers. These
  are my raw notes from day one.
layout: post
---

## Alice Goldfuss - The Container Operator’s Manual

Containers are generally presented in theory, Alice tells us how they work in real-life. Alice is an SRE at GitHub and has run Docker in production for 3.5 years, so knows a bit about containers in the wild!

1) Containers have strengths.

 - Stateless applications / processes

2) Containers have weaknesses.

 - Stateful applications / databases
Don't containerise databases - use cloud services

3) Containers need friends.

 - Multiple tools, vendors and products required to manage, deploy, network, monitor etc.

4) Containers need headcount

 - You need a whole team of engineers (6-8 people ideally) to build a container platform:
  - operations
  - deployments
  - tooling
  - monitoring
  - kernel
  - network
  - infosec
  - internal adoption
  - project manager

> Do you want containers, or a blog post?!

## Dan Persa - First Steps as a Lead (⚡️ talk)

@danpersa

Dan is an engineering lead at Zalando, based in Berlin.

> Dealing with people problems is much more interesting than dealing with development problems

The responsibility of tech leads varies by company, from a technical lead role to a line management role. It is important to understand the role at your company and whether it fits your career goals.

Dan had three months of intense mentoring from an experienced tech lead at Zalando as part of a transition process from engineer to lead.

Dan's tips on how to learn fast:
 
 1) get a mentor
 2) _apply_ what you read in books
 3) reflect on your past - how you were managed

Trust instead of control:

 1) earn the respect of the team through pair-programming
 2) regular 1:1s
 3) transparency around performance evaluations

The lead's role is to help the team discover solutions to challenges, not to solve them yourself.

Not taking a decision is a decision in itself.

Give feedback as soon as possible, with a balance of positive and constructive feedback. Always ask for feedback in return.

## Alexandra Hill - The art of giving and receiving code reviews gracefully (⚡️ talk)

Code reviews are a key factor in improving:

 - functionality
 - readability
 - meaintainability
 - scalability

But, they can be a big cause of conflict.

Low impact issues can be automated away.

Dual concerns model for conflict resolution.

Solutions to improve code reviews:

1) Pair program
2) Discsuss tasks prior to implementation
3) Don't silo codebases
4) Ensure that everyone reviews and everyone is reviewed

Reviewers can raise by a grade or two.

Use 'we' instead of 'you'. Ask questions instead of making statements. Don't make demands of people or use challenging language.

Don't forget to give positive feedback.

## Pia Nilsson - Growing teams to continuously deliver

@pia_nilsson

Increasing flow in the back-end continuous delivery squad:

1) WIP limits to increase focus, but also increased stress as engineers focussed on finishing tasks, even when delays were out of their control.
2) TDD & DDD 
3) Pairing & Mob programming

"Yes, and" - never say "No" or "but".

Non-violent communication method.

Objectives and key results (OKR).

Despicable design. Define the worst possible experience.

## Menno van Slooten - How I learned to stop worrying and love meetings

@mennovanslooten

> Becoming a lead: the subtle art of not making a difference.

1) Let go of programming - chasing your old job prevents you from seeing the value in what you _are_ doing
2) If you attend a meeting your developers don't have to, so they can focus on what they love to do
3) Learn to love interruptions - they are opportunities to help people

How do you say no??

## Jenny Duckett - Building sustainable teams to handle uncertainty

@jenny_duckett

Have a single clear goal for your team, reiterate it constantly. Use it to add context to tasks.

[Mobbing](https://gdstechnology.blog.gov.uk/2016/09/08/our-top-12-mob-programming-tips-and-thoughts/)

Use every task as an opportunity for the developer to grow & learn.

> Make yourself dispensable

Don't insulate your team too much, make it clear where their work fits in the wider picture.