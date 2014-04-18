---
layout: post
status: publish
published: true
title: Fixing MySQL in Your MAMP Install
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 676
wordpress_url: http://www.allthingsdork.com/?p=676
date: '2012-04-07 07:13:02 -0500'
date_gmt: '2012-04-07 13:13:02 -0500'
categories:
- Tech
- linkedin
tags: []
comments: []
---
<p>I'm sure you all have had a scenario where something is broken, but you figure out some janky way to get things working. Instead of spending the extra 15 minutes it would take to do the damn thing properly, you continue to live in this pseudo-functioning world. The problem is infinitely worse when it's just "your dirty little secret". Nobody else cares or even uses the functionality so why bother?</p>
<p>Well, I've been that way with <a href="http://www.mamp.info/en/index.html">MAMP</a> for a long time now. For those that don't know, MAMP (Mac, Apache, MySql, PHP) is a one click solution for setting up a web development environment on your Mac. I don't remember when I started using it, but I know it's been a lot longer than I should be comfortable admitting.</p>
<p>For some reason I've yet to look deeper into why MAMP creates its MYSQL socket inside of its own directory path, <em>/Applications/MAMP/tmp/mysql/mysql.sock</em>. Normally this isn't a big deal, but if you want anything else on your box to interact with MySQL, chances are it will be looking for MySQL's socket file in the standard <em>/tmp/mysql.sock</em> location. The error you'll typically see is <em>(2002, "Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)")</em>.</p>
<p>That's not a major problem though. You can just create a symbolic link in the <em>/tmp</em> directory by starting MySQL via MAMP and then executing <em>sudo ln -s /Applications/MAMP/tmp/mysql/mysql.sock /tmp/mysql.sock</em>. For <strong>YEARS</strong> I've been doing this after every reboot. More accurately, I've been launching MAMP, launching whatever app I'm working on, getting the error message and THEN executing this command. Today I finally got fed up with it and decided to actually figure out how to get this to happen automatically. It took me all of 10 minutes and I'm frustrated that I hadn't broke down and done this task sooner.</p>
<p>In the MAMP application folder <em>/Applications/MAMP/bin</em> there are two files, <em>startMysql.sh</em> and <em>stopMysql.sh</em>. The scripts are just executing the start and stop commands for the MySQL daemon. Those commands have a parameter called <em>--socket</em>. Simply change the path for that parameter from <em>/Applications/MAMP/tmp/mysql/mysql.sock</em> to <em>/tmp/mysql.sock</em>. Remember to do this in both files and voila. You'll never have to create a symbolic link for MySQL again.</p>
<p>I'm hoping that most of you aren't as lazy as I am and solved this problem a long time ago. But in case you haven't, you're welcome.</p>
