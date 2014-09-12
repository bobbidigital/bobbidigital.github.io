---
layout: post
title: My New Understanding of the MVC Pattern
comments: true
author: Jeff
---

I'm relatively new to the Rails community. I come from the Python/Django world, but I've been enjoying the transition, except for one minor part; Models.

When I dig around looking for info on how to structure my code, I keep running into [Best Practices](http://www.sitepoint.com/10-ruby-on-rails-best-practices/) that advocate for a skinny controller/fat model pattern. The idea being that the model contains most of the program logic. I feel like an ass-hat because I'm the new guy but this sounds crazy to me, and [others definitely agree](http://joncairns.com/2013/04/fat-model-skinny-controller-is-a-load-of-rubbish/). Why limit ourselves to three class types?

I've started to move some of my logic into separate classes that are not connected to a model or a controller. They're utility classes that deal with external sources of data that don't need to be persisted and definitely don't fit the role of the controller. In fact, their primary purpose is fetching of data from other sources, to be consumed elsewhere. With that use case in mind, I was a bit surprised when I mentioned this to a few programming buddies and it seemed like they hadn't thought of it. While we couldn't come up with a compelling reason why this was wrong, I was a little perturbed that it wasn't something regularly done. So now I have a generically named folder 'classes' to house some of these items.

I've been doing some research on [MVC purely as a design pattern](http://www.tomdalling.com/blog/software-design/model-view-controller-explained/) and I realize that I've been making one fatal mistake that's limiting my usage of the pattern. 

**Model != Persistence**. 

The problem I often run into is that my models are shaped based on how I store them in the database. But sometimes how I store an object isn't necessarily how I want to interact with the object. I end up traversing a bunch of relationships via the ORM. But if my actual storage strategy changes, I suddenly have to update code everywhere that doesn't necessarily care with how the data is saved. But in reading more about MVC, my model doesn't **have** to mirror my storage, as long as the model knows how to persist the object. 

I'll be playing around with inserting an additional layer of abstraction for my models to allow me to interact with the object in its logical form, as opposed to its actual form in the database.

We'll see how it goes