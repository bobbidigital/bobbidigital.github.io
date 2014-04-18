---
layout: post
status: publish
published: true
title: Airport Extreme and XBox Live
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
excerpt: "So I've got the Airport Extreme base station from Apple. If I had eyes into
  the future I probably would have never bought it. It's seems to be much less configurable
  than your standard Linksys or Netgear router, but I digress. The problem that I
  have is when I try to play a game on XBOX live, a lot of times I couldn't connect
  to the game or I'd get the error saying \"The match you requested is no longer available\".\r\n\r\nTurns
  out that it wasn't REALLY my Airport Extreme, but more my Motorola 2210 DSL cable
  modem. I don't know the specifics of the issue, but from what I understand the 2210
  also has a built in DHCP server. So as a result of this you end up becoming double
  NAT'd. The DHCP server inside the Motorola modem assigns a NAT address to the Airport
  Extreme and the Airport Extreme does the same to the client machine, most notably
  the XBOX 360. As a result this causes your XBOX live to fail it's NAT section of
  the XBOX Live test. (It doesn't actually fail, but reports back a status of STRICT
  as opposed to OPEN) To fix this we need to get a Public IP assigned to the Airport
  Extreme Base Station. (AEBS)\r\n"
wordpress_id: 319
wordpress_url: http://www.allthingsdork.com/?p=319
date: '2008-04-12 22:11:20 -0500'
date_gmt: '2008-04-13 02:11:20 -0500'
categories:
- Random
tags: []
comments:
- id: 30113
  author: Tom
  author_email: darosa321@hotmail.com
  author_url: ''
  date: '2008-08-18 01:53:24 -0500'
  date_gmt: '2008-08-18 07:53:24 -0500'
  content: I couldn't connect to the website it just said safari could not find, iv
    Been trying to fix my nat for months
- id: 44546
  author: Brian
  author_email: bridietzen@charter.net
  author_url: ''
  date: '2008-12-17 01:58:23 -0600'
  date_gmt: '2008-12-17 07:58:23 -0600'
  content: "Thanks so much for this post.  My modem config didn't have the &acirc;&euro;&oelig;Let
    LAN device share Internet address&acirc;&euro;\x9D option, so I reconfigured the
    Base as a pppoe, and the xbox is having no NAT problems.  Also, no problems with
    any computer that I can see so far.  \r\nThanks again.\r\n\r\nps. Will this affect
    my iMac's ichat, or any other functions of the computer?"
- id: 44572
  author: Jeff
  author_email: jeff@allthingsdork.com
  author_url: http://www.allthingsdork.com
  date: '2008-12-17 06:50:51 -0600'
  date_gmt: '2008-12-17 12:50:51 -0600'
  content: "Hi Brian -\r\n\r\n No you shouldn't see any other issues with the iMac.
    Any problems you would encounter would most likely happen with Internet connectivity
    as a whole. If you're up, you should be golden!\r\n\r\n\r\n\r\nTony - IF You still
    read this blog shoot me an e-mail via Contact Me. I TOTALLY missed your comment
    and would love to help you. If you still need it."
- id: 63043
  author: Josh
  author_email: joshmiles666@hotmail.com
  author_url: ''
  date: '2009-02-07 14:14:30 -0600'
  date_gmt: '2009-02-07 20:14:30 -0600'
  content: "Hi Jeff,\r\n\r\nI'm have a similar setup as you-a motorola 2210 modem
    > AEBS > xbox 360 via ethernet cable through the LAN ports and i've been trying
    for months to get my NAT setting off strict. I really have no idea where to go
    because every time i try a tutorial it'll explain how i need to set certain things,
    but not everything. I've been on the phone with apple and bellsouth and they were
    no help. So basically i was wondering if you could give me a breakdown of how
    i need to have the settings for my modem, AEBS, and my xbox 360. Any help would
    be greatly appreciated.\r\n\r\nThanks, \r\nJosh."
- id: 64145
  author: Kristi
  author_email: richardskristi@hotmail.com
  author_url: ''
  date: '2009-02-11 00:06:29 -0600'
  date_gmt: '2009-02-11 06:06:29 -0600'
  content: My modem is a Zhone 6211-I3 I am using the airport extreme as a router.
    I have three computers connecting wirelessly to the router and I currently have
    my apple tv and xbox 360 plugged into the back of the router. My xbox has been
    giving me a moderate nat. I am not very computer savy can you please help me if
    possible. Once the tech guys heard I was using a router they basically refused
    to help me.
- id: 67953
  author: Gordy
  author_email: gordy_mac@mac.com
  author_url: http://gordymac.net/
  date: '2009-02-19 19:32:11 -0600'
  date_gmt: '2009-02-20 01:32:11 -0600'
  content: "It worked! Thank you so much. I linked you.\r\n\r\nhttp://gordymac.net/2009/xbl-vs-strict-nats/"
- id: 80005
  author: Chris
  author_email: Candujar16@gmail.com
  author_url: ''
  date: '2009-03-23 19:39:04 -0500'
  date_gmt: '2009-03-24 01:39:04 -0500'
  content: i'm not having a NAT issue, because when i connect directly to the modem
    i have  no issues getting onto Xbox Live. i have an Airport Extreme Base connected
    to my modem and my Xbox is connected to AEBS. it was working before about a month
    ago with no issues at all and then i turned it on and suddenly it didn't work
    anymore. i did not have any special settings before, like port mapping. i guess
    a walkthrough of what i should do now would be goo, or any other advice
- id: 90112
  author: Dave
  author_email: Dave@planthreeband.com
  author_url: ''
  date: '2009-04-21 20:25:58 -0500'
  date_gmt: '2009-04-22 02:25:58 -0500'
  content: Thanks for this post!! I'll come back if it doesn't work. Peace!
- id: 90447
  author: lance
  author_email: yursoghetto@yahoo.com
  author_url: ''
  date: '2009-04-24 15:12:14 -0500'
  date_gmt: '2009-04-24 21:12:14 -0500'
  content: hey ive been having a problem with my NAT set to strict for quite sometime
    now i called at&amp;t and xbox they couldnt help me i have a motorolla 2210 and
    i dont use a router i connect it directly to my xbox and then directly to my computer
    when i use that... if anyone could help me out with some steps (i dont know much
    about computerS) it would be GREATLY appreciated. thanks -lance
- id: 103065
  author: Jeff Meuth
  author_email: jamefx@yahoo.com
  author_url: ''
  date: '2009-11-17 20:31:22 -0600'
  date_gmt: '2009-11-18 02:31:22 -0600'
  content: "Sorry to bother youi am using a hughes net HN9000 and i have a huge problem
    connecting to the market place gives me the error 800something not able to connect
    to marketplace, please help i would love to play live and never have because i
    have given up on this and yes i have airport extreme would a simple fix be getting
    a gaming router like the 4500 from d-link i would love it if you could help.\r\nJeff"
- id: 105557
  author: DuckPuppy
  author_email: paikens@gmail.com
  author_url: http://www.duckpuppy.com
  date: '2010-02-16 19:06:24 -0600'
  date_gmt: '2010-02-17 00:06:24 -0600'
  content: Instead of using a DHCP reservation, just set the 360 to not use DHCP and
    assign it a static IP.  DHCP is nice for laptops that move from network to network,
    but if it&#39;s in your house and never leaves (like a desktop PC or game console)
    just skip DHCP on that device and go static.
- id: 105717
  author: wintergiles
  author_email: benwintergiles@gmail.com
  author_url: ''
  date: '2010-03-20 23:45:23 -0500'
  date_gmt: '2010-03-21 04:45:23 -0500'
  content: This worked.. but my equipment is different. I have the xbox connecting
    wirelessly to the AEBS via 802.11n (latest black wireless adapter). The AEBS is
    connected via ether to a d-link 504t.<br><br>So I set the xbox to a static ip,
    using the normal wireless settings to get it on the network. Then tested that
    using the xbox console to make sure it was hitting the internet. (still had moderate
    NAT reporting)<br><br>Then, switch the 504t to bridge.<br><br>Input the adsl login
    details into the AEBS.<br><br>Opened all the necessary ports in the airport utility
    software:<br>for ALL, set the private IP address to the IP address of the xbox<br><br>3074,
    public and private, UDP and TCP<br>88, Public and private, UDP<br>80, Public and
    private TCP<br>53, public and private, UDP and TCP<br>3330, Public and private
    UDP<br><br>give the whole thing a kick in the guts and voila! no more moderate
    NAT. <br><br>The problem was the adsl modem double NAT ing the whole shebang.
- id: 105891
  author: 50 ft Ethernet Cable
  author_email: billysamolano@yahoo.com
  author_url: http://www.50ftethernetcable.net
  date: '2010-04-27 18:10:26 -0500'
  date_gmt: '2010-04-27 23:10:26 -0500'
  content: That&#39;s the great article! I just pass &#39;n read it, two thumbs up!
    ;)
- id: 105897
  author: Joe
  author_email: None
  author_url: http://profiles.yahoo.com/u/KAUBRESUM4XHVS2W2BNMPQKRII
  date: '2010-05-09 16:27:46 -0500'
  date_gmt: '2010-05-09 21:27:46 -0500'
  content: You&#39;re a saint, Jeffery!! This video really helped me out a lot. My
    modem&#39;s GUI is a little different than your&#39;s but I was able to configure
    it as well as my AEBS. Now my xbox live&#39;s nat went from strict to open.
- id: 105898
  author: mafo5000
  author_email: mafo5000@yahoo.com
  author_url: ''
  date: '2010-05-11 03:26:15 -0500'
  date_gmt: '2010-05-11 08:26:15 -0500'
  content: THANK YOU!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
- id: 105899
  author: mafo5000
  author_email: mafo5000@yahoo.com
  author_url: ''
  date: '2010-05-11 03:25:56 -0500'
  date_gmt: '2010-05-11 08:25:56 -0500'
  content: THANK YOU!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
---
<p>So I've got the Airport Extreme base station from Apple. If I had eyes into the future I probably would have never bought it. It's seems to be much less configurable than your standard Linksys or Netgear router, but I digress. The problem that I have is when I try to play a game on XBOX live, a lot of times I couldn't connect to the game or I'd get the error saying "The match you requested is no longer available".</p>
<p>Turns out that it wasn't REALLY my Airport Extreme, but more my Motorola 2210 DSL cable modem. I don't know the specifics of the issue, but from what I understand the 2210 also has a built in DHCP server. So as a result of this you end up becoming double NAT'd. The DHCP server inside the Motorola modem assigns a NAT address to the Airport Extreme and the Airport Extreme does the same to the client machine, most notably the XBOX 360. As a result this causes your XBOX live to fail it's NAT section of the XBOX Live test. (It doesn't actually fail, but reports back a status of STRICT as opposed to OPEN) To fix this we need to get a Public IP assigned to the Airport Extreme Base Station. (AEBS)<br />
<a id="more"></a><a id="more-319"></a></p>
<h2>The Easy Fix</h2><br />
The easy fix is to go into your modem configuration and to change a particular setting. First connect to your modem by connecting to http://192.168.1.254    This should bring you to your Motorola configuration page. Go to the Configuration page and look for an option called "Let LAN device share Internet address?". In some setups that's it, finished. Save the changes, restart the cable modem, AEBS and XBOX and you could be golden. An easy way to check is to run your XBOX Live test again from the XBOX dashboard. Your NAT test should report "OPEN". If it doesn't then chances are you need to do the following steps.</p>
<h2>The Hard Fix</h2><br />
The hard fix is to force your AEBS to handle the PPPoE authentication, which will allow it to be assigned a public IP with an open NAT translation. You have to know your AT&amp;T login and password before you go any further. If you don't have it, don't continue.</p>
<p>Login to the Motorola modem and set your modem to Bridged Ethernet mode. This will basically turn the cable modem into a forwarding device, with the endpoint being your AEBS. Now connect to your AEBS system and configure it to use PPPoE, with your AT&amp;T username and password as the authentication options. Make sure you DON'T specify DNS servers or Domain Names. Restart the cable modem, restart the AEBS and you should be golden. Just hit www.google.com real quick to make sure the connection is good. After that run your XBOX test again and the NAT should return as OPEN.</p>
<h2>Port Forwarding</h2><br />
In some rare cases you may need to do some Port Forwarding as well. The ports you'll need to forward are:<br />
&acirc;&euro;&cent;	UDP 88<br />
&acirc;&euro;&cent;	UDP 3074<br />
&acirc;&euro;&cent;	TCP 3074</p>
<p>You'll probably want to reserve a DHCP address for your XBOX however. Anytime the AEBS gets updated it reboots and as a result loses the DHCP client table. This results in your XBOX getting a new IP Address every time the AEBS gets rebooted. Which subsequently is required in order to do Port Forwarding so it's a vicious catch 22. You'll probably want to use your XBOX's MAC address. Easiest way to get this is to check your XBOX's IP address and then in the AEBS configuration under Advanced, in the Logging Tab and clicking the Log and Statistics button. Then click the DHCP Clients list and find the XBOX's IP Address and jot down the MAC address.</p>
<p>This was just a brain dump while it was fresh. I'm sure I missed something. Feel free to drop me a line if you need more help.</p>
<p>UPDATE: I've also created a quick screencast of the action too.</p>
<p><object width="400" height="300" data="http://vimeo.com/moogaloop.swf?clip_id=3263920&amp;server=vimeo.com&amp;show_title=1&amp;show_byline=1&amp;show_portrait=0&amp;color=&amp;fullscreen=1" type="application/x-shockwave-flash"><param name="allowfullscreen" value="true" /><param name="allowscriptaccess" value="always" /><param name="src" value="http://vimeo.com/moogaloop.swf?clip_id=3263920&amp;server=vimeo.com&amp;show_title=1&amp;show_byline=1&amp;show_portrait=0&amp;color=&amp;fullscreen=1" /></object><br />
<a href="http://vimeo.com/3263920">Airport Extreme and XBOX Live</a> from <a href="http://vimeo.com/bobbydigital">Jeffery Smith</a> on <a href="http://vimeo.com">Vimeo</a>.</p>
