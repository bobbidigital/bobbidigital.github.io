---
layout: post
status: publish
published: true
title: Brew is Failing with Crazy Error
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 837
wordpress_url: http://www.allthingsdork.com/?p=837
date: '2014-04-13 13:45:55 -0500'
date_gmt: '2014-04-13 19:45:55 -0500'
categories:
- Tech
tags:
- django
- homebrew
- OS X
comments: []
---
<p>If you're on Mavericks and you're using Homebrew, you may have experienced a weird error message.</p></p>
<pre><code>/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/2.0.0/rubygems/core_ext/kernel_require.rb:45:in `require': /usr/local/Library/Homebrew/download_strategy.rb:88: invalid multibyte escape: /^\037\213/ (SyntaxError)<br />
</code></pre></p>
<p>This seems to be caused by an update to Ruby version 2.0 as part of Mavericks. All you need to do is make sure that Homebrew points specifically to the 1.8 version of Ruby.</p></p>
<p>Edit /usr/local/bin/brew</p></p>
<p>Change the first line from</p></p>
<pre><code>#!/usr/bin/ruby<br />
</code></pre></p>
<p>to</p></p>
<pre><code> #!/System/Library/Frameworks/Ruby.framework/Versions/1.8/usr/bin/ruby<br />
</code></pre></p>
<p>Run a brew update afterwards. If brew update works, you're good to go. If it fails, you might need to go nuclear on this bitch. Understand this will probably trash any custom formulas you have.</p></p>
<pre><code>cd /usr/local<br />
git reset --hard origin/master<br />
git clean -df<br />
</code></pre></p>
<p>Hopefully that solves your problem.</p></p>
