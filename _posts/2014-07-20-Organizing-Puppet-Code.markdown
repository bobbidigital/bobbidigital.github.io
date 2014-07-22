---
layout: post
title: Organizing Puppet Code
comments: true
author: Jeff
---

I feel like every team I talk to, at some point decides they need to blow up their Puppet code base and apply all of the things they've learned to their new awesome codebase. Well, we're at that point in my shop and there's a small debate going on about how to organize our Puppet modules.

This is really not meant to be a mind-blowing blog post, but more of a catalog of thoughts for me as I make my argument for separate repositories for each Puppet module. A few background items.

* We'll be using the Roles/Profiles pattern. What I'm calling "modules" are the generic implementations of technologies. These are the modules I'm suggesting go into separate repositories. I'm OK with profiles and roles co-existing in a single repository.
* We're coming from a semi-structured world where all modules lived in a single SVN Repository. Our current deployment method for Puppet code is a *svn up* on the Puppet Master.
* We'll be migrating to Git (specifically [Stash](https://www.atlassian.com/stash))
* We'll have multiple contributors to the code base in 2 different geographic locations. (Chicago and New York for now) The 2 groups are new to each other and haven't been working together long.

I think that's all the housekeeping bits. My reasons for keeping separate Git repositories per modules are not at all revolutionary. It's some of the same arguments [people have been writing](http://garylarizza.com/blog/2014/02/17/puppet-workflow-part-1/) about on the web for awhile now.

## Separate Version History##
As development on modules move forward, the commits for these items will be interspersed between commit messages like "Updating AJP port for Tomcat in Hiera".  I know tools like [Fisheye](https://www.atlassian.com/software/fisheye/overview) (which we use) can help eliminate some of the drudgery of flipping through commit messages, but you know what else would help? Having a separate repo where I can just look at the revision history for the module.

##Easier Module Versioning##
With separate repositories, we can leverage version numbers for each release of the module. This allows us to freeze particular profiles that leverage those modules on a specific version number until they can be addressed and updated. With two disparate teams, this allows them to continue forward with potentially disruptive development, while other profiles have time to update to whatever breakage is occurring. 

##Access to Tools##
Tools like [Librarian-Puppet](http://librarian-puppet.com) and [R10K](https://github.com/adrienthebo/r10k) are built around the assumption that you are keeping your Puppet modules in separate repositories. I haven't done a deep dive on the tools yet, but from what I can tell, using them with a single monolithic repository is probably going to be a bit of a hurdle.

##Easier Merging/Rebasing and Testing##
The Puppet code base is primarily supported by the Systems team. The world of VCS is still relatively new to the Systems discipline. As we get more comfortable with these tools, we tend to make some of the same mistakes developers make in their early years. The thing that comes to mind is commit size and waiting too long to merge upstream. (Or REBASE if that's your thing) Keeping the modules in separate repositories tightens the problem space your coding for. If you need create a new parameter for a Tomcat module, a systems guy will probably

1. Create the feature branch
2. Modify the Tomcat module to accept parameters
3. Modify the profiles to use the parameters
4. Test the new profiles
5. Make more tweaks to the tomcat module
6. Make more tweaks to the profiles
7. Test
8. Commit
9. Merge

With separate modules, the problem space gets shrunken to "Allow Tomcat to accept SHUTDOWN PORT as a parameter".  We've removed the profile out of the problem scope for now and have just focused on Tomcat accepting the parameter. Which also means you need a new, independent way to test this functionality, which means tests local to the module. ([rspec-puppet](http://rspec-puppet.com) anyone?) This doesn't even include the potential for merge hell that could occur when this finally does get committed and pushed to master.
Now I'm not naive. I know that this **could** theoretically happen even with separate modules, but I'm hoping the extra work involved would serve as a deterrent. Not to mention that gut feeling you get when you're approaching a problem the wrong way.

#In favor of a Single Repository#
I don't want to discount that there could be **some** value in managing all your code as a single repository. Here's the arguments I've heard so far.

##It complicates deployments of Puppet Code##
True that. Nothing is easier than having to execute an *svn up* command......except for running a *deploy_puppet* command. Sure you'd have to spend cycles writing a deployment script of some sort, but if that's a valid reason then we're just being lazy. I might be being terribly optimistic but it doesn't seem like a hard problem to solve. 

In addition, I've always preferred the idea of delivering Puppet code (or any code for that matter) as some sort of artifact. Maybe we have a build process that delivers an RPM package that is your Puppet code. A simple *rpm -iv* or *yum update* and we've got the magic.

##It complicates module development##
Sometimes when people are developing modules, their modules depend on other modules. I **extremely** dislike this approach, but it is a reality. You would now have to check out two separate modules and all of their dependencies in order to develop effectively. 

Truth is, this sounds like bad workflow. A single module shouldn't reach into other modules. In the rare event that it does (say your module leverages the concat module) then these dependencies shouldn't just be inferred by an include statement. They should be managed by some tool like librarian-puppet, because in reality, that's all it is. Every other language has an approach to solving dependency management ([pip](http://pip.readthedocs.org), [gradle](http://www.gradle.org), [bundler](http://bundler.io) and now [librarian](http://librarian-puppet.com)) 

#What's Next?#
With my thought process laid out with pros and cons, I still feel pretty strongly about separate repositories for each module. Another solution might be to create some scripts that manage the modules in a way that can fool the users that care into thinking that they're dealing with a single repository. But this tends to defeat some of the subliminal messaging I hope to gain from separate modules. (Even though that's probably a pipe dream)

I'll be sure to post back what becomes of all this and if the team has any other objections.
