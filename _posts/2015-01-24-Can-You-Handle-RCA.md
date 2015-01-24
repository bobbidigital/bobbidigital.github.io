---
layout: post
title: Can You Stomach Root Cause Analysis?
comments: true
author: Jeff
---

Lately I've become extremely interested in accident analysis techniques. This is largely useful in the manufacturing and transportation industries, but there has been a growing trend to adopt these types of practices in the technology arena. Think [Kanban](http://en.wikipedia.org/wiki/Kanban), [Lean Startup](http://theleanstartup.com), and the [Theory of Constraints](http://en.wikipedia.org/wiki/Theory_of_constraints) to name a few.

But accident analysis and safety digs deep into the nature of failure within a system. Some of my favorite thinkers in the field like [Sidney Dekker](http://sidneydekker.com) and [Nancy Leveson](http://sunnyday.mit.edu) have been forcing me to go beyond the surface of an issue and to dig deeper into the organizational issues that are equal contributors to failure.

Root Cause Analysis (RCA) is something that gets touted all the time in technology. When a system goes down, we're desperately trying to find out what caused things to go bad. Despite our best efforts, we never seem to go far enough with RCAs. 

One of my favorite mantras regarding root cause is that "Root cause is simply where we stop looking." We go far enough down the rabbit  hole that we simply can't explain further, don't have the will to explain further or we've reached a politically acceptable answer. (Leveson [Engineering a Safer World](http://sunnyday.mit.edu/safer-world.pdf))

So why do we go through the theater of Root Cause Analysis in technology? Because we need to explain the unexplainable. Because if we can't explain something, how can we possibly give assurances it won't happen in the future? 

The technology field has done a great job of pretending that everyone has their shit together. No one should ever have a failure that goes undetected. Anyone who isn't alerted **before** a problem happens is an idiot. These are all worthwhile goals, but they are so far away from the reality of where we are in technology. But thanks to blogs, social media and the wisdom of hindsight, gaps in system and failure monitoring is largely the result of unqualified staff. This belief is held by management, furthered by people in the industry who talk a good game and then ultimately internalized by those with [imposter syndrome](http://en.wikipedia.org/wiki/Impostor_syndrome). So we stress and we agonize over the root cause of a thing. And that's not entirely a bad thing, but here's the rub.

Lets say we get to a point where we find that the root cause was due to setting X not being set to a reasonable or correct value. That's it. We change setting X, explain how that moves up the cause of events and fixes everything had X been set to a sane value. But **why** was X set to the value it was set at? Easy, the person before us was an idiot. But is that really the case? What factors went into that decision? What organizational pressures were present that forced a more conservative value? Could we not spend the money for extra hardware that would better utilize X? Was there no time to do performance testing so we settled on the low value for X? Did our predecessor not get the training necessary to understand the impact of X? These are all questions that need to be answered to **truly** be able to do root cause analysis. And the truth of the matter is, most organizations don't have the stomach for it. 

Companies have a hard time looking themselves in the mirror and assessing themselves in an honest light. How many projects weren't given enough time to be done right? How many projects have to skip a vital phase of the testing process due to time constraints? These are the problems you run into throughout your career, across countless companies, leading one to believe it's less about the company and more about the human condition. But regardless of the source of these problems, they are all things that contribute to the cause of failure in our systems. Organizations that have operational excellence are the orgs who aren't afraid to look at themselves honestly and follow the root cause of failure, no matter where it takes them.

Next time you participate in an RCA, take it to the next level. Don't stop at the 5th "why?" Go to the 100th, or the 1000th or however long it takes to be able to show organizationally where change needs to happen. Don't absolve yourself of all responsibility, but make sure everyone knows that the failure is not yours, but the organization's as a whole.
