---
layout: post
status: publish
published: true
title: Pandas and Django
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 807
wordpress_url: http://www.allthingsdork.com/?p=807
date: '2013-10-16 22:41:25 -0500'
date_gmt: '2013-10-17 04:41:25 -0500'
categories:
- Tech
- linkedin
tags:
- django
- pandas
- data analysis
comments: []
---
<p>I've been playing around with the <a href="http://pandas.pydata.org">pandas</a> library recently. For those that don't know, pandas is a powerful data analysis library written in Python. I've never used <a href="http://www.r-project.org">R</a> before, but from what I hear, Pandas is heavily influenced by R.</p></p>
<p>My goal is to get some of my data from a Django project into Pandas so I can leverage some of its awesome features. Pandas has a few options for getting data converted to a data frame, one of pandas data types. Pandas can read tabular data, csv files and even accept a RAW SQL query.</p></p>
<p>Considering I've already got the data I want in my database, the RAW SQL query seems the way to go. There are a few projects out there to help include support for your pandas in your Django project. I haven't used it yet but the <a href="https://github.com/chrisdev/django-pandas">django-pandas</a> project looks interesting.</p></p>
<p>For my purposes though, I just needed something quick and dirty. Writing SQL queries by hand seemed silly considering all of these pretty models I have laying around, why not use them? So here's how I leverage the Django ORM to make life a <em>little</em> bit easier.</p></p>
<p>First I'll need to update the necessary libraries</p></p>
<pre><code>import MySQLdb<br />
import pandas.io.sql as sql<br />
from football.models import FantasyPoints<br />
</code></pre></p>
<p>MySQLdb is the connector library I'm using for my database. pandas.io.sql is a parser for converting query results to the pandas data frame data type. The last line is the model from my project.</p></p>
<pre><code>records = FantasyPoints.objects.filter(stat_card__season_year=2012)<br />
db = MySQLdb.connect('<dbhost>','<username>','
<password>','<database>')<br />
</code></pre></p>
<p>First I'm going to grab a query set object from the database. We'll use the query set object to produce the SQL for us. Also remember that you're query set isn't evaluated until you iterate it, so we haven't hit the database yet. The second line is setting up our DB connection object.</p></p>
<p>Now we can use the sql object to fetch our data and convert it to a data frame.</p></p>
<pre><code>df = sql.read_frame(str(records.query), db)<br />
</code></pre></p>
<p>Our QuerySet object has a property called 'query'. It holds the internals for query construction, but if you wrap it in a <a href="http://docs.python.org/2/library/functions.html#str">str()</a> function call, you'll get the raw SQL.  With that, also pass the database connection object and voila, you have a data frame object from your database.</p></p>
<h3>Caveats</h3></p>
<p>There are a few gotchas here though. For starters, the query property is not part of the Public API, so things could change. The documentation says it's safe for pickling, so it's probably not going away, but who knows how it might change. If you're going to use this approach in production code, I <strong>HIGHLY</strong> recommend you add a layer of abstraction to it. That way if it changes, yo've only got to make your modifications in a single class/function whatever.</p></p>
<p>Another gotcha is that the str() representation doesn't quote WHERE clauses that filter on strings appropriately. So lets say your query has a filter like<br />
    WHERE position = 'RB'</p></p>
<p>The query property will output the query with no quotes around RB, making the SQL syntax invalid. I haven't spent much time digging into this because I haven't had to filter on a string. With the use of Pandas, my strategy has been to pull filter as little as possible in SQL and do my slicing and dicing in Pandas. (And caching the data frame for later reuse)</p></p>
<p>With these two big gotchas, your mileage may vary. I happen to do a lot of work in the IPython Notebook, which makes this approach very quick and simple for me.</p></p>
<p>Oh and speaking of IPython and Django projects, if you are using notebook, you'll want to check out the <a href="https://github.com/django-extensions/django-extensions">Django Extensions</a> module. It allows you to launch a notebook with all of your Django Project variables in tact. Any hoot, I've babbled long enough.</p></p>
<p>Happy Hacking</p></p>
