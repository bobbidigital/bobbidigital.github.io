---
layout: post
status: publish
published: true
title: Why I Hate Stack Overflow (and maybe you should too)
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 680
wordpress_url: http://www.allthingsdork.com/?p=680
date: '2013-01-26 22:32:31 -0600'
date_gmt: '2013-01-27 04:32:31 -0600'
categories:
- Tech
- linkedin
tags:
- python
- programming
- stackoverflow
- open source
- learning
comments: []
---
<p>I hate <a href="http://www.stackoverflow.com">Stack Overflow</a>. I hate it the same way I hate pizza. Not because of what it is, but because of what it makes me. In our new world of connectivity and huge indexes of data, there isn't much out there that can't be answered with a small exercise in Google-fu. Sometimes an answer is what you're looking for. Just think of all those times you tried to remember the name of that <a href="https://www.google.com/search?q=who+is+the+bald+crazy+guy+in+lost&aq=f&oq=who+is+the+bald+crazy+guy+in+lost&aqs=chrome.0.57j62j64.3603&sourceid=chrome&ie=UTF-8#hl=en&safe=off&tbo=d&sclient=psy-ab&q=bald+guy+from+lost&oq=bald+guy+from+lost&gs_l=serp.3..0.8224.10199.0.10344.18.12.0.5.5.0.125.1089.10j2.12.0.les%3B..0.0...1c.1.F1zYXUkhMA0&pbx=1&bav=on.2,or.r_gc.r_pw.r_cp.r_qf.&bvm=bv.41524429,d.eWU&fp=e5351287a4c2a4a0&biw=1731&bih=1128">bald guy from LOST</a>. On those drunken nights when you're arguing about what <a href="http://starwars.wikia.com/wiki/Jek_Tono_Porkins">Porkin's</a> last words in Star Wars were, answers are <strong>awesome</strong>. But when you're a developer, the answer is nothing more than a shortcut.</p></p>
<p>I was working on a little side project the other day and I was trying to figure out the best way to handle HTTP Redirection in the <a href="http://docs.python.org/2/library/urllib2.html">urllib2</a> library in Python. Of course I did a Google search to get my answer and per usual, the first few links were to Stack Overflow questions. I found myself going through the results and scrolling right to the answers section. I'd speed read through the answer, determine if it was sufficient for my needs and move on to the next question. I was looking for an answer, when what I really should have been looking for is knowledge.</p></p>
<p>Too often in tech we use and leverage things that we don't fully understand. We've become complacent in a world where "magic" is real and somethings just sort of happen. But in an open source environment, there's no room or excuse to have a lack of understanding about the tools you're using. I'm not saying you should be able to rewrite the regular expression engine, but just having a basic understanding of how things works doesn't just give you the answer, but it gives you <strong>knowledge</strong>. In my case, after the third or fourth answer, I said "Why not just look at the source code Jeff?" So that's what I did. Boy was I surprised to see everything I needed to know about my problem listed right in the beginning of the source file in the comments section. I was amazed at how little "magic" was in use. But I was inspired by the design and the elegance of it all. (Elegance is a relative term based on experience. I'm sure surgeons in the 30's though hacksaws were elegant)</p></p>
<p>To make a long story short, I got my answer and some knowledge. I used a lighter version of the library's design to solve a larger problem I had been facing with my own project's implementation. I sure as hell wouldn't have gotten that from Stack Overflow.</p></p>
<p>The moral of the story is, make sure you know when you should be looking for answers and when you should be looking for knowledge. Whenever you have the time, the latter is always the better option.</p></p>
<p><strong>p.s.</strong> <br/>But in case you were just looking for an answer, you need to override the HTTPRedirectHandler</p></p>
<pre>
import urllib2<br />
class NoHTTPRedirection(urllib2.HTTPRedirectHandler):<br />
        def http_error_302(self,req,fp,code,msg,headers):<br />
            #Whatever you want to do for the redirect. I ignore it and just return<br />
			return                                                                                                                           </p>
<p>        http_error_301 = http_error_303 = http_error_307 = http_error_302 </p>
<p>opener = urllib2.build_opener(NoHTTPRedirection)<br />
urllib2.install_opener(opener)<br />
</pre></p>
