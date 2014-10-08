---
layout: post
title: Feature Toggles in Puppet
comments: true
author: Jeff
---

When we're performing Puppet changes, we try to work within the framework of some sort of [SDLC](http://en.wikipedia.org/wiki/Systems_development_life_cycle). We're in the process of migrating to [Stash](https://www.atlassian.com/software/stash) from [SVN](http://subversion.apache.org), so our processes are a bit in flux. But one problem we run into constantly is how to balance long running feature branches and separation of Puppet code that is still in development or testing.

The systems team works very closely with the developers, sometimes with our changes being dependent on one another. An example is when we move a file from being hosted on our web servers, to being served by S3. It requires a coordinated change of the Apache config to handle the redirects and the development code that automatically handles the population of S3. While this is being tested, we need to have to different copies of the Apache configuration for the site.

A) - Copy in production where files are located on the web server itself.

B) - Copy in test that handles a redirect to the S3 location.

The testing that takes place may take a day or it may take weeks. The longer testing takes, the more drift there is between my Puppet development branch and the master branch which is getting pushed to production regularly.  I could just be a rebase monster while this is being tested, but sooner or later, I'll fail in my responsibility and I'll have some awful merge waiting to happen. I needed a better way and the best thing I could come up with was some form of [Feature Toggle](http://martinfowler.com/bliki/FeatureToggle.html).

With a feature toggle, I have the ability to release some code, without all nodes receiving that code path. More specifically for my use case, I can commit code to master, without fear of it actually being executed. This is often leveraged in [Continuous Integration environments](http://www.thoughtworks.com/continuous-integration) to prevent incomplete code from impacting production.

With Puppet I decided to implement something very similar using if blocks and Puppet Enterprise console variables. When I'm developing something I put my resource declarations in a block like so

	if $sitemap_redirect_feature == 'enabled' {
		// Puppet Resource Declarations	}
	else {
		// Default activities	}
	
Then in Puppet Enterprise console, I'll assign the variable sitemap_redirect_feature to enabled in the console. If you're not a Puppet Enterprise customer or aren't using the console, you could also specify it in a hiera lookup, with a default value.

	hiera('sitemap_redirect_feature', 'disabled')
	
This makes it easier to assign to groups of servers based on your hiera configuration.

Because of the way Puppet variables are evaluated, any node that doesn't explicitly set the variable will follow the else path.

The plus side to this is while you're figuring out exactly how resources should be laid out, you can still commit to master without fear of breaking anything. (Just make sure you do all your static analysis so that your Puppet code is at least valid)

Once your testing is complete and your ready to push the changes to production, you simply remove your updated resource declarations from the if/else block so that they're always executed. Delete the if/else block and push your code. 

I've been using this pattern for a few weeks now and so far it is working out pretty well. I may refine the approach as I run into new hurdles.

