---
layout: post
status: publish
published: true
title: How and why tmp_table_size and max_heap_table_size are bounded
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 804
wordpress_url: http://www.allthingsdork.com/?p=804
date: '2013-10-08 08:54:49 -0500'
date_gmt: '2013-10-08 14:54:49 -0500'
categories:
- Tech
tags: []
comments: []
---
<p>tl;dr -- If your query exceeds the lowest of these 2 settings in size, it will write the temp table to disk. These 2 parameters need to be updated together.</p></p>
<p><a href="http://www.pythian.com/blog/how-and-why-tmp_table_size-and-max_heap_table_size-are-bounded/">How and why tmp_table_size and max_heap_table_size are bounded</a>: ""</p></p>
<p>(Via <a href=""></a>.)</p></p>
