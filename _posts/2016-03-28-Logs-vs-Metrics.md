---
layout: post
title: Logs vs Metrics
comments: true
author: Jeff
---

I constantly struggle with the idea that a log entry and a metric are not the same thing. Both provide value, but they're telling different stories. The problem is that the distinction is a lot like pornography. [I'm not 100% sure how to define it](https://en.wikipedia.org/wiki/I_know_it_when_I_see_it). 

In my shop, our applications emit a **lot** of data. Now some of you are reading and thinking that this is a first world problem in the technology space; I get that. But the problem is when I try to use the right tool to evaluate that data. Should this go into a log file to be aggregated by a tool like ELK or Splunk? Or should this just be a tick that fires and is sent to a metrics collector like Graphite? How do I articulate that choice to a developer?

Let's look at Twitter for example. Let's say they want to track tweets per second. For our purposes the options are 

* Log to a file when a tweet happens.  That log is shipped to an aggregator. Then a log search tool evaluates the log messages (because there could be other log messages there) does some math and then displays it. 
* The application uses some transactional annotation around the "new tweet" functionality. That sends an "event" type metric with some additional metadata and fires it off to a metric service. 

Both are conceptually the same thing, but the log file approach seems dirty to me. Other than the benefit of some abstractions, the core tenants of both approaches is the same. My discomfort must lie in the intent of these two things.  

A log entry should give you information or detail about a **specific** event where as a metric should just let you know that an event occurred. 

An example of a good log message

* Tweet number 238472 was submitted successfully by user @darkandnerdy at 11:05am
* User DarkandNerdy has failed a login attempt. The user has 4 concurrent login failures 

An example of a metric

* 11:05 - tweet submission successful
* 11:15 - Failed login attempt

The specificity that a log message allows is what makes it valuable. But more importantly as an Operations person, that specificity should be allowed to be tunable. I only need that specificity when a problem arises. I shouldn't be forced to have logging set to a low level (like INFO) just to have an idea of how the system is performing. In normal Operation, I want my log file to contain anomalies, not stacks of information telling me that everything is ok. (And if that is the case, maybe those logs need some separation from General log messages)

Through the process of writing this blog post I've become much clearer on how I feel about these two things. My "thesis statement" if you will, would be this:

Logs messages are notifications about events as they pertain to a specific transaction within the application. Metrics are notifications that an event occurred, without any ties to a transaction. 

Ok so what's the difference? Well again putting on my Operations hat, metrics can be incredibly smaller because they convey considerably less information. They're also extremely easier to evaluate. Both of these points have impact around how we store, process and retain metrics. 

A log file however, gives you details on a transaction which may allow you to tell a more complete story for a given event. The transactional nature of the log message in aggregate, gives you much more flexibility in terms of surfacing information (not just data) about the business. 

So now that I think I've cracked my first world problem, I'd pass on a bit of advice to folks. Any data is better than no data. If things are preventing you from having a decent separation of things, just **HAVING** the data makes a huge difference. Once you have it, you can argue over the semantics. :-)

