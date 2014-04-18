---
layout: post
status: publish
published: true
title: Getting Solaris Installed on Dell 2970/2950
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
excerpt: "Ahh, well if you&acirc;&euro;&trade;re reading this post then chances are
  you&acirc;&euro;&trade;re ready to shove a fork in your own eye. That&acirc;&euro;&trade;s
  ok though, because even with one eye I will try my best to walk you through the
  gruesome process that exists in order to marry the Dell 2970/2950 and Solaris.
  It's painful, but it is do-able. I would highly recommend using different supported
  hardware, but who knows. You might be restricted into the Dell hardware by forces
  outside your control. Well know that you've finally found an ally!\r\n"
wordpress_id: 249
wordpress_url: http://www.allthingsdork.com/?p=249
date: '2008-01-24 18:16:00 -0600'
date_gmt: '2008-01-24 22:16:00 -0600'
categories:
- linkedin
tags:
- linkedin
comments:
- id: 34234
  author: Rutger
  author_email: rutger@illian.net
  author_url: ''
  date: '2008-09-21 13:10:02 -0500'
  date_gmt: '2008-09-21 19:10:02 -0500'
  content: "I nearly killed myself, then the server, and then the guys at SUN not
    putting a relatively old controller (Perc5) and ethernet NIC (broadcoms) into
    the ISO !!! Couldn;t figure it out while at the datacenter, hapily reading your
    post.\r\n\r\nWill try to convert the machine from FreeBSD to Solaris sometime
    in the near future..."
---
<p>Ahh, well if you&acirc;&euro;&trade;re reading this post then chances are you&acirc;&euro;&trade;re ready to shove a fork in your own eye. That&acirc;&euro;&trade;s ok though, because even with one eye I will try my best to walk you through the gruesome process that exists in order to marry the Dell 2970/2950 and Solaris. It's painful, but it is do-able. I would highly recommend using different supported hardware, but who knows. You might be restricted into the Dell hardware by forces outside your control. Well know that you've finally found an ally!<br />
<a id="more"></a><a id="more-249"></a><br />
First problem you&acirc;&euro;&trade;re going to run into is this. If you&acirc;&euro;&trade;re using the Dell 2970 you&acirc;&euro;&trade;ll notice that there is some kind of problem with the IDE controller drivers. Your CD-ROM drive will only work up until the install of Solaris actually begins. (Major bummer, I know) So the first thing I&acirc;&euro;&trade;d have you do is track down an external CD-rom drive that connects via USB. We used a Sony DVD-R/CD-RW and Solaris recognized it fine, so any unit will probably do. If you&acirc;&euro;&trade;re using the Dell 2950 then chances are you should be OK with the drive you currently have.</p>
<p>So I&acirc;&euro;&trade;m assuming you have the Solaris media already. The next thing you&acirc;&euro;&trade;ll need is a driver for you&acirc;&euro;&trade;re Perc5/e RAID Controller. Yup, the Dell card that came with your box does NOT have a Solaris driver built in. So when you go to install you get that nasty message &acirc;&euro;&oelig;No Disks Found! Please check your cables&acirc;&euro;&brvbar;.&acirc;&euro; Blah blah blah. So what we need to do is get your controller card recognized. In order to do that you&acirc;&euro;&trade;ll need the Perc 5/E ITU update. You can get this from the LSI website (the manufacturer of the card) or if you&acirc;&euro;&trade;re lazy you can use the one I&acirc;&euro;&trade;m linking to <a href=http://www.allthingsdork.com/downloads/Perc5E_ITU.iso>here</a>. Now this is the ITU I used in ISO format. Depending on when you're reading this it could be very very very outdated. But if you're still reading then I'm assuming it's better than the driver you have now. Burn the ISO to a CD-rom. (For those that are unsure you can do this in Windows using Roxio or whatever you have)</p>
<p>So now you've got your USB CD-rom plugged in (for those 2970 folks) you've got your Solaris CD and you've burned the ITU ISO image to a CD rom. Lets start booting from the CD-rom drive. </p>
<p><b>NOTE FOR 2970 FOLKS:</b> Now if you're using the 2970 here's a hint. It's going to sound VERY counterintuitive. Go ahead and boot from your internal CD-rom drive. I know what I said earlier but trust me. We're going to let the boot kernel get expanded from the CD-rom drive and then swap CD's later. It's much faster this way.</p>
<p>Put the CD-rom in your internal drive and begin the boot process. Once you get to the GRUB menu select the first option in the list. If you're using the 2970 you may see a lot of errors during the boot process complaining "WARNING: /pci@0,0/pci-ide@1f,1/ide@1 (ata1)" or something similar. Ignore it for now.</p>
<p>You should get to a point where your prompted with a few options.</p>
<p>   1. Solaris Interactive (default)<br />
   2. Custom JumpStart<br />
   3. Solaris Interactive Text (Desktop session)<br />
   4. Solaris Interactive Text (Console session)<br />
   5. Apply driver updates<br />
   6. Single user shell</p>
<p>Choose option 5 to Apply Driver Updates. It's going to ask for you to put in a Floppy, or CD/DVD drive. Eject the Solaris install CD and put in the ITU cd we burned earlier. <b>NOTE FOR 2970 FOLKS:</b> At this point put the ITU CD/DVD into the EXTERNAL CD/DVD drive. I know it sounds crazy, but trust me. At this point in the install on the 2970, the IDE controller is being controlled by Solaris and the install Kernel has NO idea how to interact with it. (Those nasty warning messages from earlier)</p>
<p>Once you've got the CD/DVD in press C and watch it install that driver. Press E to end. It will then prompt you to put the Solaris CD back in the drive and hit enter. <b>NOTE FOR 2970 FOLKS:</b> You're going to want to put the Solaris CD back into the External CD/DVD drive. Again, at this point the internal CD drive is dead to you.</p>
<p>From here, the Solaris install should start and it should look quite normal to you now. My next writing will be "OK..it's installed...but i've got no Broadcom network interfaces!" If you already know how to install packages then you can just download the <a href="http://www.allthingsdork.com/downloads/BRCMbnx.pkg">Broadcom Packages</a>. </p>
