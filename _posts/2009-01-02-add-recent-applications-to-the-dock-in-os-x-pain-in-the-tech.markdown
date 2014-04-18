---
layout: post
status: publish
published: true
title: Add Recent Applications to the Dock in OS X   -- Pain in the Tech
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 491
wordpress_url: http://www.allthingsdork.com/?p=491
date: '2009-01-02 10:27:57 -0600'
date_gmt: '2009-01-02 16:27:57 -0600'
categories:
- Random
tags: []
comments: []
---
<p>The team over at the <a href="www.paininthetech.com">Pain in the Tech</a> blog have a good tip for adding a recent applications icon to the Dock. Good stuff. See the full article with screenshots <a href="http://paininthetech.com/2008/12/26/add-recent-applications-to-the-dock-in-os-x">here</a>.</p>
<blockquote>
<p>To create this stack, open the Terminal window, found under Utilities, and paste (all on one line) in the following and hit enter:</p></p>
<p><code>defaults write com.apple.dock persistent-others -array-add '{ 'tile-data' = { 'list-type' = 1; }; 'tile-type' = 'recents-tile'; }'</code></p></p>
<p>You must restart the Dock for this to take effect. Type in the Terminal window:</p><br />
</blockquote></p>
