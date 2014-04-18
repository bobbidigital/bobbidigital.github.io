---
layout: post
status: publish
published: true
title: Parsing the Contents of Mailq
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 819
wordpress_url: http://www.allthingsdork.com/?p=819
date: '2014-01-04 15:56:05 -0600'
date_gmt: '2014-01-04 21:56:05 -0600'
categories:
- Tech
- linkedin
tags:
- email
- python
- programming
comments: []
---
<p>Every so often you come across that task that you think is going to be insanely easy. But alas, you roll up your sleeves, get into the nitty-gritty and discover a twisted twisted web of minor problems. That's been my experience with the <a href="http://www.postfix.org">Postfix</a> mailq.</p></p>
<p>I wrote a <a href="https://github.com/bobbidigital/mailq">mailq log parser in Python.</a> The mail queue is where Postfix and Sendmail dump emails that can't be sent or processed for various reasons. It's a running log of entries that can be dumped out in plaintext via the <strong>mailq</strong> command. I thought this task would be simple, but a few hurdles I ran into.</p></p>
<p><strong>1. The log file is a variable line length.</strong></p></p>
<p>A record could span multiple lines. That means you can't simply iterate through the file line by line. You need to figure out where a record beings and ends. So far from my testing it appears the line length is based on the reason the mail is in the queue. Which leads me to item #2.</p></p>
<p><strong>2. Figuring out why the record is in the queue</strong></p></p>
<p>This was trivial, but it was an odd design choice. An item could be in the queue for various reasons. There is a special character at the end of the queue ID that tells you the reason it's in the queue. * means one thing, ? means another and the lack of a special character means yet another. Once you've parsed the queue id out, it's trivial to check the last character, but why not just make it a separate field?</p></p>
<p><strong>3. Different versions of Postfix have slightly different outputs</strong></p></p>
<p>As soon as I ran a test in our QA environment I learned that different Postfix versions have slight modifications to the output of the mailq command. The annoying part is that the updates aren't substantive at all, but just change for change sake as far as I can tell. Now the email address is blanketed by <> characters. The count of the number of items in the queue are in the beginning of the file instead of the end. And the text describing that number changes its wording just a tad. "Total Requests" instead of "Requests in Queue". Not very useful.</p></p>
<p><strong>4. The date doesn't include a year</strong></p></p>
<p>I mean...really? And the date isn't formatted in a MM-DD-YYYY format. It's more like "Fri Jan 3 17:30". So now you're converting text in order to find the appropriate date. This post is timely too because the beginning of the New Year is where this is really a pain. The fix I'm using so far is to assume it's the current year and then test the derived date to see if it's in the future. If it is, fall back to the previous year. This assumes you're processing the queue regularly. It's an auditor's nightmare.</p></p>
<p>None of it was terribly difficult, but more more difficult than it needed to be. It's as if they wrote the mail queue to only be parsed by humans. I'll be working on my MailQReader for a little bit because I have a need at work.</p></p>
