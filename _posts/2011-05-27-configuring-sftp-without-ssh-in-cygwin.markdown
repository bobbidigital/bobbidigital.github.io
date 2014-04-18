---
layout: post
status: publish
published: true
title: Configuring SFTP without SSH in Cygwin
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 668
wordpress_url: http://www.allthingsdork.com/?p=668
date: '2011-05-27 09:56:07 -0500'
date_gmt: '2011-05-27 15:56:07 -0500'
categories:
- Tech
- linkedin
tags:
- linkedin
- computers
- Cygwin
- SFTP
comments: []
---
<p><a name="intro"></p>
<h2>Introduction</h2><br />
</a></p>
<p>As most of you know, FTP is the devil in terms of security. It sends clear text passwords over the wire, with most users being actual system users as well. It&acirc;&euro;&trade;s telnet&acirc;&euro;&trade;s equally evil little brother. In the *nix world, it&acirc;&euro;&trade;s not that big of a deal, because you have free tools that come shipped with the OS. But in the Windows world (at least in pre 2003) there is no secure solution out of the box. With budget crunches being what they are, most managers aren&acirc;&euro;&trade;t willing to switch to an SFTP solution which can run $1000+ per license.<br />
For one of our smaller FTP implementations I decided to try and get Cygwin running on Windows, with an OpenSSH implementation. It&acirc;&euro;&trade;s not the greatest, but it is free, cheap and will execute as a service as opposed to some big control panel that needs a user logged in. (A common symptom of free Windows SFTP solutions) I also wanted to make sure that a user couldn&acirc;&euro;&trade;t get an interactive shell once they logged in, essentially giving them access to the entire machine.</p>
<p><a name="install"></p>
<h2>Cygwin Installation</h2><br />
</a></p>
<p>The first thing I had to do was go through the <a href="http://www.cygwin.com/">Cygwin</a> installation. When you go through the setup, there will be an additional section that asks you for additional packages to install. Be sure that you install the OpenSSH packages, as those will provide your SSH and SFTP server binaries.</p>
<p>Once Cygwin is installed, we&acirc;&euro;&trade;ll need to add a new user to the system to handle the SSHD process. We don&acirc;&euro;&trade;t want to execute this as Local System, due to some security issues and hurdles.  First we&acirc;&euro;&trade;ll create the user account. Drop to a command line (I&acirc;&euro;&trade;m a command line guy) and execute</p>
<pre><code>net user sshd password /add /fullname:&acirc;&euro;Cygwin SSH Daemon&acirc;&euro;</code></pre><br />
Replaced &acirc;&euro;&oelig;sshd&acirc;&euro; with whatever username you want to use and &acirc;&euro;&oelig;password&acirc;&euro; with whatever password you want. You probably also want to make sure the password doesn&acirc;&euro;&trade;t expire, but I&acirc;&euro;&trade;ll let you make that call. Next you&acirc;&euro;&trade;ll need to add this user to the Administrators group. I still haven&acirc;&euro;&trade;t been able to find out the other security needs, but I know that my implementation didn&acirc;&euro;&trade;t work until I added the user to the Admin group.  You shouldn&acirc;&euro;&trade;t worry though, we&acirc;&euro;&trade;ll be taking other precautions to ensure that the user is sufficiently limited.</p>
<pre><code>net localgroup Administrator sshd /add</code></pre><br />
Next we&acirc;&euro;&trade;ll need to assign the SSHD account some appropriate rights, as well as take away some rights. I&acirc;&euro;&trade;m using the ntrights command which can be found in the <a href="http://www.microsoft.com/downloads/en/details.aspx?FamilyID=9d467a69-57ff-4ae7-96ee-b18c4790cffd&amp;DisplayLang=en">Windows 2003 Resource Kit</a>.</p>
<p>Execute the following commands.  <a href="&acirc;&euro;">Command Definitions</a></p>
<ul>
<li>ntrights +r SeAssignPrimaryTokenPrivilege -u sshd</li>
<li>ntrights +r SeCreateTokenPrivilege -u sshd</li>
<li>ntrights +r SeDenyInteractiveLogonRight -u sshd</li>
<li>ntrights +r SeDenyNetworkLogonRight -u sshd</li>
<li>ntrights +r SeDenyRemoteInteractiveLogonRight -u sshd</li>
<li>ntrights +r SeIncreaseQuotaPrivilege -u sshd</li>
<li>ntrights +r SeServiceLogonRight -u sshd</li><br />
</ul><br />
You&acirc;&euro;&trade;ll notice that we&acirc;&euro;&trade;ve chosen to deny the user interactive logon capabilities, meaning he is just a service account at this point.</p>
<p>Now we&acirc;&euro;&trade;ll want to setup one of the System Variables. Right click on My Computer and go to Properties. Click the &acirc;&euro;&oelig;Advanced&acirc;&euro; Tab and then click &acirc;&euro;&oelig;Environment Variables&acirc;&euro; on the bottom pane.</p>
<p>In the section marked &acirc;&euro;&oelig;System Variables&acirc;&euro; click New and add a variable named &acirc;&euro;&oelig;CYGWIN&acirc;&euro; and give it a value of &acirc;&euro;&oelig;ntsec tty&acirc;&euro;. Click OK, and then OK again to save your changes.</p>
<p>Now you&acirc;&euro;&trade;ll want to launch your Cygwin shell and run the SSH configuration script.</p>
<pre><code>ssh-host-config</code></pre><br />
You&acirc;&euro;&trade;ll want to answer Yes to all questions except the question &acirc;&euro;&oelig;This script plans to use cyg_server, Do you want to use a different name?&acirc;&euro;  You should enter the name of the user account we created earlier. (In our exampled it was &acirc;&euro;&oelig;sshd&acirc;&euro;)</p>
<p>Next you&acirc;&euro;&trade;ll need to run</p>
<pre><code>cyglsa-config</code></pre><br />
<strong>Warning: This will require a reboot!!</strong> This command enables Cygwin to use the Local Security Authority to help authenticate users. Once the command is complete, be sure to reboot your system. If your service fails to start after the reboot <a href="#ServiceFail">check the services failure section</a>.<br />
Next we need to create the group and passwd file. These files are necessary for Cygwin users to authenticate. They are the Unix counterpart to the SAM database.</p>
<p>Execute the command</p>
<pre><code>mkpasswd &acirc;&euro;&ldquo;l > /etc/passwd<br />
mkgroup &acirc;&euro;&ldquo;l > /etc/passwd</code></pre><br />
You should be able to now accept incoming SSH connections. Make sure that all necessary firewall ports are open. Using <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/">Putty</a> or your other favorite SSH client, connect to your machines IP with a username and password. Be sure that you&acirc;&euro;&trade;ve setup another user besides the SSHD user.</p>
<p><a name="UserPrevent&acirc;&euro;"></p>
<h2>Preventing a User from Logging In</h2><br />
</a></p>
<p>If you want to prevent a user from completely logging in, you can modify the /etc/passwd file in Cygwin. Chances are you don&acirc;&euro;&trade;t have VI installed, so your best bet is to browse to your Cygwin installation directory in explorer and open the passwd file in the etc folder. The very last portion of each line represents what shell should be launched for the user. The default is &acirc;&euro;&oelig;/bin/bash&acirc;&euro;. If there&acirc;&euro;&trade;s a user you don&acirc;&euro;&trade;t want accessing the system, change that to &acirc;&euro;&oelig;/bin/false&acirc;&euro;. Voila. The user can&acirc;&euro;&trade;t login via SFTP or SSH. However, you will have to change this every time you regenerate the password file. (Which is why this solution is only good for small implementations)</p>
<p><a name="SFTPOnly"></p>
<h2>Only allowing SFTP for a User</h2><br />
</a></p>
<p>Edit the /etc/passwd file on the system by browsing to it either in explorer or by launching VI in a Cywin window. Change the default shell for the user (the last portion of the user line) from &acirc;&euro;&oelig;/bin/bash&acirc;&euro; to &acirc;&euro;&oelig;/usr/sbin/sftp-server&acirc;&euro;.  This will make SFTP the users default shell.</p>
<p><a name="chroot"></p>
<h2>Setting up a CHROOT for a User</h2><br />
</a></p>
<p>There is no true CHROOT concept in Cygwin, because it is implemented using Windows DLLs. If you need to do CHROOT, I&acirc;&euro;&trade;ve heard that <a href="http://sublimation.org/scponly/wiki/index.php/Main_Page">scponly</a> is a solution that works and can be compiled in Cygwin. I&acirc;&euro;&trade;ll be trying this soon, so details will follow.</p>
<p><a name="remarks"></p>
<h2>Closing Remarks</h2><br />
</a></p>
<p>Let&acirc;&euro;&trade;s be clear. Cygwin is not the ideal SFTP solution for Windows. Sometimes however, circumstances will warrant its use. The above solution without the CHROOT has one <strong>major</strong> flaw. The user has complete access to the disk. While they can&acirc;&euro;&trade;t necessarily execute code directly, there are things they could do to make life bad for you. You need to be diligent in your security setup if you intend to do this. Hopefully my CHROOT experience will go well and I can share the details with you at another time.</p>
