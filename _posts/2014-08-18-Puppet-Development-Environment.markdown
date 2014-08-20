---
layout: post
title: My Puppet Development Environment
comments: true
author: Jeff
---

I was in attendance at [Puppet Camp Chicago](http://puppetlabs.com/events/puppet-camp-chicago-0) today and had some really awesome conversations with people. It's always worthwhile to hear how people are approaching similar problems to yours. It was also nice to get a chance to meet some of the developers of my favorite Puppet modules, but I digress.

One of the conversations that came up was what our local development process looked like for Puppet. Many people are attempting to find the right mixture of process and tools to help develop their infrastructure. With this in mind, I figured it might be worthwhile to share my developer setup. YMMV.

**VIM** - VIM is my editor of choice. Of course saying you use VIM is like saying "I have a car".  Nobody just uses VIM these days. There's always some plugins that get mixed in there, my setup is no different.

* [vim-ruby](https://github.com/vim-ruby/vim-ruby) - VIM Ruby is a nice plugin for all types of fun, helpful bits. Check it out.

* [NERDTree](http://www.vim.org/scripts/script.php?script_id=1658) - A great plugin that adds some file browsing capabilities to VIM.  Well worth it to avoid buffer hell.

* [Powerline](https://github.com/Lokaltog/powerline) - A great add-on for VIM, zsh, and bash that adds an awesome status bar to your VIM interface. The git status in the toolbar is extra helpful. 

* [tmux](http://tmux.sourceforge.net) - Tmux isn't really a VIM plugin, but it is essential to my workflow. Being able to create multiple windows, split panes and easily navigate amongst them with keyboard shortcuts.

* Custom VIM Functions - I have one main custom function that I use hevaily for linting. The function determines whether the file is a Puppet (*.pp), JSON(*.json) or ERB (*.erb) file and runs the appropriate linter. Below is a copy of it.

<pre>
function LintFile()  
     let l:currentfile = expand('%:p')  
      if &ft == 'puppet'  
         let l:command = "puppet-lint " . l:currentfile  
     elseif &ft == 'eruby.html'  
         let l:command = "erb -P -x -T '-' " . l:currentfile . "| ruby -c"  
     elseif &ft == 'json'  
         let l:command = 'jsonlint -q ' . l:currentfile  
      end  
      silent !clear  
         execute "!" . l:command . " " . bufname("%")  
   endfunction  
   map <c-L> :call LintFile()<cr>
   </pre>
   
##Virtual Machine Setup##
   
   My local development environment consists of two virtual machines, a Puppet master and a Puppet client. I'm using [Virtualbox](https://www.virtualbox.org) for virtualization, but really any VM tool should be fine. 
   
   The nice thing with having a virtual puppet client on your desktop is that you can snapshot it to get your VM back to an initial state. So before you do any development on the Puppet client, make sure you [take a snapshot](http://www.virtualbox.org/manual/ch01.html#idp55591632) so that you can get back to a clean starting point.
   
On the Puppet Master VM you'll want to [create a shared folder](https://www.virtualbox.org/manual/ch04.html#sharedfolders) in Virtualbox or your VM Manager of choice.  Point the shared folder to whatever folder holds your Puppet manifests on the local machine. Now [mount the shared folder](https://www.virtualbox.org/manual/ch04.html#sf_mount_manual) in your VM so that it's accessible within the Virtual Machine. You should now have access to your Puppet manifests on your local machine, via the Virtual Machine.
	
Last but not least, modify your [modulepath](https://docs.puppetlabs.com/references/latest/configuration.html#modulepath) in the virtual Puppet master and add the shared folder path to the modulepath. By adding the shared folder to your modulepath, you can develop your Puppet manifests on your local machine, with all your tools without the need to develop inside the VM or to sync files from your local machine to your VM.

##Remote Puppet Development##

Occasionally you might hit a use case that isn't testable on a local machine and you need to test it on a Puppet master in your pre-prod environment. (You do have a pre-prod environment right?) When this situation comes up it's nice to have [Puppet Environments](http://puppetlabs.com/blog/git-workflow-and-puppet-environments) setup. Most people use them in a dynamic fashion, but you can definitely use them statically. (And with SVN) After you've created the environments, it's just a matter of getting your files to the path on the remote server. Rsync is a great tool for this as it allows you to get your files to the remote server for testing, without the need to actually commit code that you're not sure will work yet. (Which in some environments might trigger a long, time consuming series of automated checks and builds)

That's pretty much it for my development environment. I should also mention that if you're working on a Mac, it might be worth checking out [Dash](http://kapeli.com/dash), which is an awesome developer documentation tool. It basically sucks down the Docsets of various programming languages and tools. (Puppet being one of them)

At some point I'll probably write a follow up post to detail our actual development and deployment workflow. Hope this helps some poor soul out there on the web.