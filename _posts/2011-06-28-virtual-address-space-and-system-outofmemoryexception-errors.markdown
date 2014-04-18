---
layout: post
status: publish
published: true
title: Virtual Address Space and System.OutofMemoryException errors
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 672
wordpress_url: http://www.allthingsdork.com/?p=672
date: '2011-06-28 16:10:23 -0500'
date_gmt: '2011-06-28 22:10:23 -0500'
categories:
- Tech
- linkedin
tags:
- linkedin
- system administration
- outofmemory exception
- troubleshooting
comments: []
---
<p>Sometimes in an environment you get one of those pesky error messages that only shows up occasionally. Recently for me, it&acirc;&euro;&trade;s been the System.OutofMemory exception. The error was being thrown by an IIS Website the server was hosting. My troubleshooting was specific to an IIS Application pool, but hopefully this post will give you some food for thought if you&acirc;&euro;&trade;re experiencing a similar situation.</p>
<p>The first thing was to do the obvious and check to make sure we weren&acirc;&euro;&trade;t actually out of memory. These days there are about 1000 different warning signs letting you know the server is close to being out of memory. Not to mention you&acirc;&euro;&trade;ll probably see performance issues across the board as opposed to a single application. So if you&acirc;&euro;&trade;ve got enough memory, why would you get an OutOfMemory exception? </p>
<p>Well first, let&acirc;&euro;&trade;s back up a bit and talk about the virtual memory manager of Windows. If you&acirc;&euro;&trade;ve never done any programming or operating system work, you may not know this. All processes are given their own virtual address space. What this means is that the executing process is ignorant to the actual memory available to the system. As far as the process is concerned, it has a whopping 4 gigabytes of memory. The upper 2 gigabytes of the stack are "reserved" by the operating system, while the lower 2 gigabytes are used by the process. These values can change based on boot switches, 64bit Windows or other settings, but we&acirc;&euro;&trade;ll use these numbers for our example.</p>
<p>The process is a bit ignorant to things like paging. The process simply requests memory and treats it as if all memory is physical ram, leaving those cumbersome paging and mapping details to the operating system. The other important thing to remember is that memory is allocated in contiguous chunks. That means if your program is requesting 5 megabytes of memory, not only must there be 5 megabytes of memory available, but there must be 5 megabytes of adjacent memory locations available. So even if you&acirc;&euro;&trade;ve got 1 gigabyte of memory available, if it&acirc;&euro;&trade;s totally fragmented into small chunks, you may not have enough contiguous memory available, which in turn will cause the System.OutofMemory exception. </p>
<p>How do you defragment a process&acirc;&euro;&trade;s virtual memory map? I&acirc;&euro;&trade;m not sure that you do. If you restart the process, a new map is created, but this isn&acirc;&euro;&trade;t always feasible. In reality, most of your applications won&acirc;&euro;&trade;t have this problem, but long running processes, for example IIS, might run into this situation. If you dump all your websites into your DefaultApp pool, it&acirc;&euro;&trade;s quite possible that all those applications are fragmenting the address space to the point where you can&acirc;&euro;&trade;t load large DLLs, such as the AjaxControlToolkit.dll file. (The culprit in my exercise)</p>
<p>Sometimes it&acirc;&euro;&trade;s difficult to get an idea of what the process virtual map looks like. I&acirc;&euro;&trade;ve discovered a helpful tool called <a href="http://www.hashpling.org/asm/">Address Space Monitor</a>. The application will let you know the largest amount of contiguous memory available to your process along with some other helpful bits of information. </p>
<p>I combined this, with another helpful tool called <a href="http://technet.microsoft.com/en-us/sysinternals/bb896645">Procmon</a>. With Procmon you can monitor all types of activities, including attempted file loads into memory. I simply ran Procmon with a filter for dll files that were being loaded by the process I was having trouble with to get an idea of what was going on when the OutofMemroy exception was being thrown. After seeing a 5.6 megabyte file being loaded by a process with 2 megabytes of contiguous address space available, it was pretty clear what my problem was.</p>
<p>This write-up is somewhat specific to my problem, but I hope it at least has given you some food for thought for troubleshooting your own issue.</p>
