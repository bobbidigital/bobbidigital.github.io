---
layout: post
status: publish
published: true
title: .NET MVC Invoking Controller Action With NULL Parameter Values
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 670
wordpress_url: http://www.allthingsdork.com/?p=670
date: '2011-06-10 10:54:55 -0500'
date_gmt: '2011-06-10 16:54:55 -0500'
categories:
- Tech
- linkedin
tags:
- linkedin
comments: []
---
<p>I've been working on a web site using C# and the Microsoft MVC framework. So far I'm liking what I'm seeing, but I'm still digging into some of the actual implementation details. There are some things that happen with MVC that look like standard stuff you've seen before, but actually behave quite differently.</p>
<p>One of the hurdles I (and several other people) was facing was that I had a controller action, with a parameter, but the parameter was being passed into the controller with a value of NULL. Phil Haack put together a nice <a href="http://haacked.com/archive/2008/03/13/url-routing-debugger.aspx">Routing Debugger</a> utility to see how your routes were being interpreted by the MVC Framework. Everything looked good, I could see that the ID value was being properly populated, but my Controller action parameter still had a null value.</p>
<p>After doing some research I discovered that even though your Controller Action looks like a regular method signature, the way parameters are passed is actually quite different.  The parameters are actually key/value pairs that exist in the HTTPRequest Object. If you've defined the following controller method signature</p>
<pre><code><br />
public ActionResult SaveADDomain(string Name, string Desc, string Id)<br />
</code></pre></p>
<p>The MVC Framework will look for keys named "Name", "Desc" and "Id" and populate the corresponding variables with the key's value. If the key doesn't exist, null is instead populated in the variable. I believe the collection for the key/value pairs is stored in the HTTPRequest  Params property, but don't quote me on that just yet. So how do we define these key value pairs? In the Global.asax file of course!</p>
<p>The Global.asax file is where the Routes for your application are registered. The default file should look something like the following:</p>
<pre><code><br />
      public static void RegisterRoutes(RouteCollection routes)<br />
        {<br />
            routes.IgnoreRoute("{resource}.axd/{*pathInfo}");</p>
<p>            routes.MapRoute(<br />
                "Default", // Route name<br />
                "{controller}/{action}/{id}", // URL with parameters<br />
                new { controller = "Home", action = "Index", id = UrlParameter.Optional } // Parameter defaults<br />
            );</p>
<p>        }<br />
</code></pre></p>
<p>You'll notice in the routes.MapRoute call, there is a URL path definition of {controller}/{action}/{id}.  The {id} is the beginning of the parameters calls. So if you wanted to also have a parameter like "sortorder" or something like that, you could modify the route pattern to look like {controller}/{action}/{id}/{sortorder}.  Or you could use it to rename the {id} to something else.</p>
<p>Hope this helps someone out there.</p>
