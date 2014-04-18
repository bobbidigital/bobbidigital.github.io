---
layout: post
status: publish
published: true
title: Even Non-Profits Can Virtualize with VMWare ESXi
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 506
wordpress_url: http://www.allthingsdork.com/?p=506
date: '2009-01-11 10:19:29 -0600'
date_gmt: '2009-01-11 16:19:29 -0600'
categories:
- linkedin
tags:
- linkedin
comments:
- id: 52778
  author: Sharif
  author_email: manjisan@gmail.com
  author_url: ''
  date: '2009-01-13 09:08:51 -0600'
  date_gmt: '2009-01-13 15:08:51 -0600'
  content: I have to say in my experiences using VMWare, it has been a blessing and
    curse. Developing MSIs or WISE packaging in this environment can be a harrowing
    experience albeit a fulfilling one if all works well, which it did) especially
    across various OSes. Now if only I could use it for Video Conferences. Pzah.
---
<p>In my day job we, like many other companies, have been struggling with the problem of data center sprawl and the expenditures that go along with that. One of the first things that we looked at was server virtualization but with budgets getting tighter and tighter in today's economic climate we certainly couldn't spend money to save money. It was then that we stumbled upon VMWare ESXi.</p>
<p>Server virtualization has been a hot trend in the IT field lately. For those that don't know server virtualization is basically the process of emulating the hardware layer of a machine through software with the goal of being able to create several instances of a machine on a single server. So one machine could be used to emulate multiple complete machines including networking and their own storage allocations.</p>
<p>One of the great benefits to virtualization is the consolidation of servers. Now an adequately outfitted machine can serve as multiple servers which are isolated from one another. For example in our lab environment at the office we have a single server hosting 9 virtual servers with room to spare! We save money on power (because there's only 1 physical machine as opposed to 9) and we save on space. (For the same reasons)</p>
<p>VMWare ESXi is a Virtual Machine Server implementation based on the popular ESX architecture created by VMWare. The software is a small footprint, bare metal install of the virtualization software. The ISO will perform the install after answering just a few questions and embeds itself into the physical server's firmware. The install also will detect all compatible hardware and configure it appropriately, with the keyword being compatible. So far our common incompatibility point has been with storage arrays, specifically the Dell MD3000 arrays, so you'll want to make sure to check the <a href="http://www.vmware.com/resources/compatibility/search.php?client=safari&rls=en-us&sa=X&oi=spell&resnum=0&ct=result&cd=1&q=VMWare%2520ESX%2520Hardware%2520compatibility&spell=1">Hardware Compatibility List</a> prior to beginning the install. Once the software is installed, virtual servers are configured and deployed via a Windows GUI based interface. ESXi will allow you to define resource pools for memory, cpu utilization and disk usage. This can keep a particular virtual machine from running rampant and impacting other virtual machines on the same physical server.</p>
<p>Now for the major selling point of <a href="https://www.vmware.com/tryvmware/?p=esxi&rls=en-us&q=vmware%20esxi%20download&ie=UTF-8&oe=UTF-8">VMWare ESXi</a>. This great technology is available to you absolutely free, no strings attached. You won't have access to any of the really fancy features available in some of the other virtual suites, but you can absolutely do serious production work with ESXi and is instantly an option for companies or organizations of any size.</p>
<p>Besides the benefits already listed you've also got the added benefit of being able to run multiple operating systems on a single piece of hardware. A virtual server can host virtual machines running, Linux, Windows and Solaris (to name a few) all at the same time. This can really lead to cost savings for companies with restrictive IT budgets. ESXi also supports virtual switches, so you could simulate an entire network on a single machine. This is great for lab testing or development work.</p>
<p>If you work for a company and you've been tossing the idea of playing around with sever virtualization now you can with no risk. If you're that tinkering developer that wishes he had more environments to play with, now you can do it and you can do it for the lowest price ever possible. I highly recommend you check out <a href="https://www.vmware.com/tryvmware/?p=esxi&rls=en-us&q=vmware%20esxi%20download&ie=UTF-8&oe=UTF-8">VMWare ESXi.</a></p>
<p><!-- Technorati Tags Start --></p>
<p>Technorati Tags:<br />
<a href="http://technorati.com/tag/virtual%20server" rel="tag">virtual server</a>, <a href="http://technorati.com/tag/virtualization" rel="tag">virtualization</a>, <a href="http://technorati.com/tag/vmware" rel="tag">vmware</a>, <a href="http://technorati.com/tag/vmware%20esxi" rel="tag">vmware esxi</a><br />
</p><br />
<!-- Technorati Tags End --></p>
