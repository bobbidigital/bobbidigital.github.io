---
layout: post
status: publish
published: true
title: Invalid Syntax When Using or Installing S3Cmd Tools
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 812
wordpress_url: http://www.allthingsdork.com/?p=812
date: '2013-12-15 17:56:30 -0600'
date_gmt: '2013-12-15 23:56:30 -0600'
categories:
- Tech
tags:
- python
- programming
- s3
comments: []
---
<p>I installed the <a href="http://s3tools.org">s3 tools</a> on a new machine that was spun up for a testing environment. I was quickly greeted with an ugly error message.</p></p>
<pre><code> utc = datetime.datetime(*dateS3toPython(s3timestamp[0:6],tzinfo=pytz.timezone(&acirc;&euro;&tilde;UTC&acirc;&euro;&trade;))  ^<br />
SyntaxError: invalid syntax<br />
</code></pre></p>
<p>Not a very helpful error if you're new to Python. I'm not 100% sure what the problem is here, but it appears that Python version 2.5.2 (and older) have a problem with list expansion combined with a keyword argument.</p></p>
<p>Here's some quick dummy code I put together to illustrate.</p></p>
<h2>Python 2.5.2</h2></p>
<pre><code>def test(*args, **kwargs):<br />
    print "Received Args"<br />
    print "Received Kwargs"</p>
<p>>>> arg=(1,2,3,4)<br />
>>> test(*arg, test='bar')<br />
      File "<stdin>", line 1<br />
        test(*arg, test='bar')<br />
              ^<br />
SyntaxError: invalid syntax<br />
>>> test(1,2,3,4,test='bar')<br />
Received Args<br />
Received Kwargs<br />
</code></pre></p>
<p>But running this same code on Python 2.6.8 (which is in the Redhat Repos) doesn't produce the problem at all.</p></p>
<p>So the easy fix is to upgrade your version of Python. I've reported the bug to the S3cmd team to address. My guess is they'll just require a newer version of Python. Their current version test only looks for 2.4 or better. Which is probably out date.</p></p>
