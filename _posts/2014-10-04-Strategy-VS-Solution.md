---
layout: post
title: Strategy vs Solution
comments: true
author: Jeff
---

In the technology arena, things are constantly changing and new technologies are being spun out at a rapid rate. The problem is that as technologist, we're eager to try out the new hotness, with [Docker](https://www.docker.com) being the new darling child. Just [ask Google](https://www.google.com/search?btnG=1&pws=0&q=docker+hype&gws_rd=ssl) about the hype cycle behind Docker.

I'm not going to debate the anointed position of Docker. It is a very cool and incredibly useful technology. But what I do take issue with is using Docker for the sake of using Docker, without any real examination of the problems that are trying to be solved. Docker gets trotted out as a strategy, rather than taking its rightful place as a solution *for a strategy*.

Containerization of your application may or may not be a straight forward exercise. You could spend weeks getting things tuned and setup in a way so that you can now deploy your application via Docker. You're living the dream of developing on your desktop and having that same container move all the way through your pipeline into production. But if your build still takes 90 minutes, is it worth the effort? Have you actually solved your pain point?

I'm not dismissing the other intangibles that Docker offers, but I'm a big fan of the [Theory of Constraints](http://en.wikipedia.org/wiki/Theory_of_constraints). Optimizing for anything other than the bottleneck is just a waste. 

It sounds like I'm picking on Docker, but it's just an easy example because of its current popularity. But I'll give an example closer to home. 

I'm working on a [Fantasy Football site](http://www.leaguelytics.com) in my spare time. One of my *strategies* is to collect information from all of the various sites that provide fantasy data projection. 

Notice how my strategy is devoid of any specific technology or implementation. That's how a strategy should be defined. In clear terms that don't hint towards a specific solution or direction.

Well, I lost site of that and immediately jumped to the solution. I wrote a series of scrapers to go out to various websites and pull down the information, without any thought to my actual strategy. I jumped to the solution because it's an easy thing to do as an engineer.

Fast forward a few weeks and I'm spending more time fixing the scrapers and coding defensively against changes to the source website, instead of continuing development of my application. But if I think about my *strategy* I could probably come up with a few quick solutions.

* [Mechanical Turk](https://www.mturk.com/mturk/welcome) - I could hire someone for probably less than $10 dollars to have someone manually enter the data into a CSV document. Writing a CSV importer is a lot simpler than an HTML scraper.
* [Fantasy Data](http://fantasydata.com/nfl-stats/fantasy-football-weekly-projections.aspx) - While a bit pricier, I could also pay for an API end point to provide me with a bunch of data. ESPN, CBS, and Yahoo all have similar services available at varying prices.

Between the 3 options that I briefly described (Mechanical Turk, Fantasy Data and a custom scraper), the mechanical turk option makes the most sense for me. It's inexpensive, delivers the value I'm looking for and has the  lowest amount of effort on my side, allowing me to focus on my core product.

The moral of the story is, remember to evaluate **why** you want to implement a technology. The strategy should be separate from the solution so that you can make sure your addressing your pain points.