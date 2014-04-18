---
layout: post
status: publish
published: true
title: Protect Production Environments from Test Environments with IPTables
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 810
wordpress_url: http://www.allthingsdork.com/?p=810
date: '2013-10-31 20:42:47 -0500'
date_gmt: '2013-11-01 02:42:47 -0500'
categories:
- Tech
- linkedin
tags:
- security
- iptables
- development environments
- firewall
comments: []
---
<p>Thanks to the flexibility of virtual machines, you've probably found yourself with a clone of a production machine being deployed to a test environment. There are a variety of reasons to do this. Maybe you're preparing for an application upgrade, tracking down a particularly nasty bug or building a clone of your production environment for QA.</p></p>
<p>The fear is always "How do I prevent the clone from acting on production?" It's a very real fear, because it's easy to miss a configuration file. In an ideal scenario you'd have the test environment on a different network segment that has no connectivity to the production environment. But if you're not that lucky, then there's iptables to the rescue!</p></p>
<p>With <a href="http://en.wikipedia.org/wiki/Iptables">iptables</a> you can use the below command to prevent your test host from connecting to production.</p></p>
<pre><code>iptables -A OUTPUT -m state --state NEW -d <ipaddress> -j DROP<br />
</code></pre></p>
<p>This command will prevent any new connections from being initiated FROM your test server to the server specified by . This is handy because it still allows you to make a connection FROM the banned production box to the target test box. So when you need to copy those extra config files you forgot about, it won't be a problem. But when you fire up the application in the test environment and it tries to connect to prod, iptables will put the kibosh on it.</p></p>
<p>If you're super paranoid, you can get execute</p></p>
<pre><code>iptables -A OUTPUT -d <ipaddress> -j DROP<br />
</code></pre></p>
<p>This will prevent any outbound packets at all from going to .</p></p>
<p>Don't forget that the iptables command doesn't persist by default, so a reboot will clear added entries. To save the entries and have them persist, execute:</p></p>
<pre><code>service iptables save<br />
</code></pre></p>
<p>Good luck!</p></p>
