---
layout: post
status: publish
published: true
title: Those Pesky .DS_STORE files
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 133
wordpress_url: http://www.allthingsdork.com/?p=133
date: '2007-07-11 16:57:05 -0500'
date_gmt: '2007-07-11 20:57:05 -0500'
categories:
- Random
tags: []
comments:
- id: 1532
  author: Brandi
  author_email: eratos.daughter@gmail.com
  author_url: ''
  date: '2007-07-27 13:08:51 -0500'
  date_gmt: '2007-07-27 17:08:51 -0500'
  content: You said running around like a hamster shitting... heheheh. You totally
    brightened my day with that quip. Now I remember why I like you so much. :)
- id: 1828
  author: Captain Kirk
  author_email: alphanull@gmail.com
  author_url: ''
  date: '2007-08-12 05:12:08 -0500'
  date_gmt: '2007-08-12 09:12:08 -0500'
  content: '*shakes fist* MAAAAAAAAAAAAC!'
- id: 1831
  author: jeff
  author_email: jeff@allthingsdork.com
  author_url: http://www.allthingsdork.com
  date: '2007-08-12 20:52:46 -0500'
  date_gmt: '2007-08-13 00:52:46 -0500'
  content: Wrath of Khan...the greatest of many William Shatner performances. It brings
    a tear to my eye.
- id: 105450
  author: Generic levitra.
  author_email: ''
  author_url: http://www.esnips.com/user/order-levitra-9gav
  date: '2009-12-31 08:56:20 -0600'
  date_gmt: '2009-12-31 14:56:20 -0600'
  content: |-
    <strong>Levitra....</strong>

    Levitra dangers. Levitra and alcohol use. Levitra. Levitra pen....
- id: 105454
  author: Soma sen arizona.
  author_email: ''
  author_url: http://www.esnips.com/user/buy-soma-2jxm
  date: '2010-01-01 18:05:02 -0600'
  date_gmt: '2010-01-02 00:05:02 -0600'
  content: |-
    <strong>Soma sen....</strong>

    Soma overnight. Soma without rx. Crushing muscle relaxer soma. Soma. Buy soma online. Buy soma watson brand online 150 tablets. Soma online....
- id: 105458
  author: Xanax side effects.
  author_email: ''
  author_url: http://www.esnips.com/user/order-cheap-xanax-3sap
  date: '2010-01-02 18:13:21 -0600'
  date_gmt: '2010-01-03 00:13:21 -0600'
  content: |-
    <strong>Xanax....</strong>

    Buy xanax. Xanax no prescription. Ijijiji xanax hompage. Buy xanax without prescription. Xanax. Xanax without a prescription. Xanax side effects....
- id: 105464
  author: Viagra cialis levitra.
  author_email: ''
  author_url: http://www.esnips.com/user/order-cheap-levitra-7boi
  date: '2010-01-04 19:54:21 -0600'
  date_gmt: '2010-01-05 01:54:21 -0600'
  content: |-
    <strong>Levitra cialis viagra....</strong>

    Cheap levitra. Levitra....
- id: 105922
  author: social networking software
  author_email: ''
  author_url: http://www.social-networking-software.org/
  date: '2010-08-31 13:48:34 -0500'
  date_gmt: '2010-08-31 19:48:34 -0500'
  content: |-
    <strong>social networking software...</strong>

    Great post! I really liked the content and disposition in your topic!...
---
<p>The one problem I have using my Mac at work are those pesky .DS_Store files. For those that don't know your Mac creates a .DS_Store file in every directory it goes into. The file (Directory Services Store) is responsible for holding certain preference information about how the Finder should display that folder. If a .DS_Store file doesn't exist in that directory when you browse to it in Finder, the Finder is nice enough to create one for you.</p>
<p>Now Finder hides this file, so Mac Users are typically oblivious to it. But when you start working in a networked environment with Windows or Linux users you'll soon here people screaming "WTF are all these .DS_Store files".  Yes, our beloved OS X runs around like a hamster, shitting .DS_Store files all over the network in any folder we go to. Very easy way to piss off non-Mac users.</p>
<p>But of course there is a fix. Execute the terminal application and at a command line type the following:</p>
<p>defaults write com.apple.desktopservices DSDontWriteNetworkStores true</p>
<p>This will prevent the Finder from shitting .DS_Store files on networked drives. It's a beautiful thing isn't it?</p>
<p>Keeping Peace between Windows lovers and Mac Lovers</p>
