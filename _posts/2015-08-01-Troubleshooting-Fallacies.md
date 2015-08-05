
An outage on a large distributed system can be a very difficult thing to troubleshoot.  The pressures of an outage can often lead to making poor or shortcut decisions. When the system is down, the drive is to get the system back operational as quickly as possible. But sometimes we sacrifice process for the sake of speed.

In this frantic state, we fall victim to what I call *Troubleshooting Fallacies*. 


## #1 - Subsystems Fail All or Nothing

When we're troubleshooting an issue we start to quickly assess the potential failure points in the system that may be causing the problem. Sometimes this may happen at lightning speed at a subconscious level. For example:

* You know it's not the network because you can ping the server
* DNS isn't the problem because the hostname is resolving
* The application can connect to the database because you verified credentials and connectivity from the command line.

The list could continue, but you get the idea. The criteria we use for eliminating these subsystems is usually razor thin, ignoring the complexity within each of those sub-systems. **We behave as if the subsystem fails in totality**.  But it's quite possible that the subsystem is failing in a sort of nuanced way. Maybe only specific DNS servers are failing. Or maybe they're only failing from a specific node. Maybe the host can connect to the database, but the application is having trouble connecting, possibly due to a configuration issue.

When you begin to exhaust your options, be sure that you verify the subsystems involved as concretely as possible. Sometimes a high level pass of the subsystem simply isn't enough.

## #2 - No Errors = No Problems

When trouble starts and the resolution hasn't been narrowed down, you might call a team member from each area like, storage, networking, application developers, and site support. As each functional area signs-in, most admins have already begun rationalizing why it isn't their particular subsystem that's at fault. This sort of system bias leads the admin to perform a less than ideal verification of their system.

Instead of verifying that things are working correctly, the admin simply confirms that no errors are being thrown. But this mode of verification assumes that the admin knows every type of failure mode of the system and how it manifests itself, an unlikely reality.  This is what I call checking for errors instead of verifying success. 

Checking for errors can be a bit oversimplified if you don't believe your system is at fault. It exposes a kind of [confirmation bias](https://en.wikipedia.org/wiki/Confirmation_bias) where you may dismiss anomalous, but not necessarily damning information. Verifying success is a bit more thorough, but requires a level of preparation **before** the incident, as it will most likely require some automation. Verifying success may look like:

* Scripted versions of API calls
* Database connection tests from nodes in question
* Synthetic transactions against a web interface
* Response code verifications

Now you'll notice that most of these sound like potential monitors that should be part of the system. That is true, but a lot of these monitors would probably be implemented in the system admin's language of choice, versus the language the system is written in. (Think python vs. java) These success verification applications should try to mimic or mirror the languages and libraries used in the application to help reveal potential software incompatabilities.

## #3 - Finding the Root Cause is a Must

Root cause analysis is a tricky subject. In most of these overly complex systems, the idea of a root cause is a bed time story we tell managers to help them sleep at night. The hard truth is that the more complicated our systems become, the more nuanced are failures are. Root cause is fast becoming a thing of the past. Failure looks more like various sub-systems entering a failed state, which in turn produces a system level failure mode. Example:

1. HTTP Requests come into a web server without a timeout value
2. The HTTP requests results in database calls
3. The database is saturated, so the queries take 2-3 seconds to respond.
4. The service time of requests to the HTTP server is too long to handle the arrival rate of requests without queueing.
5. The HTTP server runs out of available threads and makes the service  completely unavailable.

Is the database the root cause?  Or is it the fact that HTTP requests are allowed to execute without a timeout value? Or maybe the HTTP server doesn't have a sufficient number of threads for peak traffic volume?

Any one of those could be a valid root cause, which means none of them are really the root cause. The lack of root cause does prevent a tidy answer for an incident report, but it does promote a more thorough understanding of your system and its various failure modes.

If your leadership insists on root cause analysis, I suggest you take that analysis as far back as possible. [You may not like where it takes you](http://www.allthingsdork.com/2015/01/24/Can-You-Handle-RCA/)

## #4 - It Should Be a Quick Fix

As problems arise, admins can repeatedly underestimated the impact of the issue. The quick fix is always around the corner, which ultimately slows down the final resolution because of a sort of haphazard, *gut feeling* approach to troubleshooting.

It's easy to be undisciplined in your troubleshooting process during an outage. The pressure is on and you leap from one potential issue to another, a lot of times without any scientific evidence to pack it up. It's imperative however that we maintain control and process, even in the face of a management mob desperate for resolution.

This of course presupposes that you have a methodology. If you don't have a process I would highly suggest looking at [the USE Method](http://www.brendangregg.com/usemethod.html) by [Brendan Gregg](https://twitter.com/brendangregg). It's a practical approach that allows you to break up a system into various components and then test those components for particular failures. 

Gregg's approach has a particular performance bend to it, but with a little bit of effort it can be adapted to suit analysis at any level of the application stack.

#Wrap Up

This list is far from exhaustive, but highlights some of the issues that teams fall victim to. Recognizing your mistakes is the first step to avoiding them. I hope to continue to expand on this list over time.