---
layout: post
status: publish
published: true
title: Postgres, Django and that Damn Clang Error
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 833
wordpress_url: http://www.allthingsdork.com/?p=833
date: '2014-04-02 19:59:55 -0500'
date_gmt: '2014-04-03 01:59:55 -0500'
categories:
- Tech
tags:
- python
- django
- postgres
comments: []
---
<p>I'm migrating to PostGres for one of my Django projects. (From MySQL) I'm writing this more as a note for myself, but if someone else finds it useful, go for it. If you've done this on a Mac, you may have seen the following errors.</p></p>
<blockquote>
<p>Error: pg_config executable not found.</p><br />
</blockquote></p>
<p>If you've found that error, then you may not have Postgres installed. If you do have Postgres installed then make sure the installs bin directory is in your path. If you don't have Postgress installed, the easiest way is <a href="http://postgresapp.com">Postgres.app</a>. After installing Postgres drop to a terminal and add a new value to your PATH.</p></p>
<pre><code>export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/9.3/bin<br />
pip install psycopg2<br />
</code></pre></p>
<p>Don't feel discouraged when this fails again. Because it probably will. The message is extremely helpful if you've got your Ph.D.</p></p>
<blockquote>
<p>clang: error: unknown argument: '-mno-fused-madd' [-Wunused-command-line-argument-hard-error-in-future]<br />
  clang: note: this will be a hard error (cannot be downgraded to a warning) in the future<br />
  error: command 'cc' failed with exit status 1</p><br />
</blockquote></p>
<p>It may not be downgraded in the future, but today is not tomorrow. So lets hack this bad boy.</p></p>
<p>Things you need:</p></p>
<ol>
<li>If you don't have it already, <a href="https://itunes.apple.com/us/app/xcode/id497799835?mt=12">download Xcode</a> and install it.</li><br />
</ol></p>
<p>1a. Drop to a terminal and install the command line tools with</p></p>
<pre><code>xcode-select --install<br />
</code></pre></p>
<ol>
<li>
<p>If you already had Xcode installed and it's version 4.2 or earlier, skip ahead to step X. If you downloaded Xcode in step 2, you'll need to install some additional compiler tools that were removed from Xcode. The best way is to use <a href="http://brew.sh">Homebrew</a>. (You are using Homebrew RIGHT?)</p></p>
<p>brew install apple-gcc42</p></li></p>
<li>
<p>Once that's complete. If this works, you're done. If not (and it probably won't) move on to step4.</p></p>
<p>pip install psycopg2</p></li></p>
<li>
<p>Set an environment flag to skip the BS compiler flags being used.</p></p>
<p>export ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future<br />
pip install psycopg2</p></li><br />
</ol></p>
<p>With any luck, that will result in a successful install.</p></p>
