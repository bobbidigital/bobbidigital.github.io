---
layout: post
title: Rethinking Stability -  Part 1 Review of In Search of Certainty
author: Jeff
comments: true
---

Stumbling through the web, I found this book club called [ReadOps](http://readops.com). It's an amazing idea and our first book to read is [In Search of Certainty](http://www.amazon.com/In-Search-Certainty-Information-Infrastructure-ebook/dp/B00ENEEWYO) by [Mark Burgess](http://markburgess.org), a seriously smart man. We're reading the book in sections and with a bit of effort, I was able to get through part 1. Below is the writeup I did for ReadOps. If you're in the IT Field, [ReadOps](http://readops.com) might be worth checking out.

***

Part 1 of this book was rough, but I promise that it gets better in the later chapters. The principle issue I have is the amount of depth that Burgess goes into to setup his arguments. There are significant correlations between his work in physics and its history, but I don't find it useful beyond the 2nd or 3rd paragraph. Now with that being said there are a few points that I find absolutely stellar.

##How We Measure Stability##
The sections on stability really challenged my thinking on how we measure stability. In general, I've always measured stability throgh the [ITSM Incident/Problem Management](http://en.wikipedia.org/wiki/Incident_management_(ITSM)) processes. But Burgess struck home for me when he says that what we're _actually_ measuring in these processes are **catastrophes**, not stability. 

If I had the right models for stability, I'd recognize the erratic memory usage patterns of the Java Virtual Machine (JVM). Those swings/fluctuations would give me an idea on the stability of the JVM. (I'm also mixing a concept he talked about in regards to scale, but that's a whole different thing) Instead, I don't pay attention to the small perturbations that lead up to the eventual OOM or long pause garbage collection. Instead the OOM triggers an incident ticket, which then gets tracked and mapped against our stability, when truth be told, stability was challenged much earlier in the lifecycle. 

I'm not sure if ITSM has controls to deal with these types of situations or not.  In my specific case above,  an incident ticket might not have been warranted due to the fact that memory usage can be self-healing through garbage collection. But without defined thresholds and historical data to trend against,  it would be easy to see miss an incident or situation where memory usage whent from 40% -> 75% -> 44%. Sure memory usage dropped significantly, but it's still up 4% from where we started. What do I do with this information? I guess that's where clearly defined thresholds come into play.

##A Stability Measurement##
With all that being said, I wonder if there's the possibility to measure stability into some abstract value or number. (Maybe this has already been done and I'm late to the party?) I think a lot about [Apdex](http://www.apdex.org/overview.html) and how much I love it as an idea. But for me, as a Systems guy, its at the wrong scale and it introduces components that I have no control over. (Namely the client browser and everything that happens inside it) What would be incredibly useful though was some sort of metric for ServerDex.  I'm imagining taking a range of values, deciding which ones fall outside the desired thresholds and applying some sort of weighted decaying average to it. (I'm literally just spitballing here) That could give Systems folk some sort of value to track against. It be nice to be able to take several of these measurements and combine them for an approximation of the stability of our system as a whole.

Ok, time for me to hit the hay.