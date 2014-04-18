---
layout: post
status: publish
published: true
title: Sorting Objects in Python
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 666
wordpress_url: http://www.allthingsdork.com/?p=666
date: '2011-05-21 09:42:39 -0500'
date_gmt: '2011-05-21 15:42:39 -0500'
categories:
- Tech
- linkedin
tags:
- linkedin
- heapsort
- minsort python
- python
comments: []
---
<p>I'm a relative newcomer to Python, but drew interest in it when looking for a framework to develop a project I've been working on. I was introduced to DJango and liked the possibilities, but figured I should do a bit more with Python before diving in. So I started working on a Python script at the office to help me parse some <a href="http://jakarta.apache.org/jmeter/">JMeter</a> log results. I'm trying to gather some statistical data on when errors occur during a load test and the JMeter reports don't seem to have quite what I'm looking for. </p>
<p>The first problem I ran into was that there are multiple threads executing the load test. As a result, the log file is not organized in a linear fashion. I've put all of the data elements of the test into objects, but now I need to sort the list based on the TimeStamp property of each object. Not to mention the list is roughly 500,000 elements long, so I need it to be somewhat efficient. (Although performance isn't a HUGE deal in this project) I opted to go with a min-heap data structure.</p>
<p>After doing some digging I came across the <em>heapq</em> library in Python. The problem was that there was no mechanism for sorting based on the property of an object. It basically would take a list of values and sort them. I really wasn't in the mood to write my own library for this project, but I figured it was worth spending some time with the problem because it would most certainly come up again in my days with Python. </p>
<p>Ultimately I discovered that the <em>heapq</em> library would also accept a tuple as a parameter, sorting based on the first element in the tuple. So the problem came down to something as simple as:</p>
<p><code><br />
	import heapq<br /><br />
	listObject = []<br /><br />
	logEntry = fetchNextLogEntry()<br /><br />
	heapq.heappush(listObject, (logEntry.TimeStamp, logEntry))<br /><br />
</code></p>
<p>Now when I iterate though my list, I'll be returned a tuple. I just need to grab the second element out of the tuple for my actual object and do my worse with it. It was pretty simple. </p>
<p>There was another option however. We could overload the comparison operators on our objects.</p>
<ul>
<li>__eq__</li>
<li>__ne__</li>
<li>__ge__</li>
<li>__gt__</li>
<li>__le__</li>
<li>__lt__</li><br />
</ul></p>
<p>By overloading these comparison operators, I can define how the comparison would take place.</p>
<pre>
<code><br />
def __le__(self,other):<br />
	return self.timestamp < other.timestamp<br />
</code><br />
</pre><br />
Now I'll need to do this for all of the comparison operators, but once I'm done I'm golden. Some people suggested doing this using the <a href="http://en.wikipedia.org/wiki/Decorator_pattern">Decorator Pattern</a> but for my needs that might be overkill. My data set won't be that dynamic and I know my needs at compile time. (Or design time as it were)</p>
<p>Also there was some chatter out there about using overloading __cmp__ , which would work, but is deprecated as of Python 3.0. Python 3.0 isn't in wide use yet and future proofing in this case is easy enough. But if you're really lazy and don't have a need for 3.0 compatibility, there's that route too.</p>
