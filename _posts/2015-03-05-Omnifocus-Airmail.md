---
layout: post
title: Airmail2 + Omnifocus
comments: true
author: Jeff
---

*Full disclosure. I've had a few drinks and should probably wait till morning to write this. But waiting is for suckers. YOLO*

I'm a big fan of [Omnifocus](https://www.omnigroup.com/omnifocus) and [Airmail](http://airmailapp.com). Together they're like peanut butter and jelly. But one thing that absolutely drives me **insane** is the way Airmail's integration works with Omnifocus.

When I convert an email in Airmail to a task in Omnifocus, it creates a task with the task name being the subject. But the body of the message (the note) actually becomes a link to the Airmail message. That's all fine and dandy, but I use Gmail as my mail provider. When I archive messages, Omnifocus seems to get confused on how to find the message based on the URL link. Rubbish. I want something simple and stupid. Enter [Applescript](http://www.macosxautomation.com/applescript/). 

With Applescript I was able to quickly write a tool that allows me to convert the body of the email message into a note in the Omnifocus task, which eliminates the need for me to keep the message around at all in my Inbox. Below is the script, but you can [check out the Gist here.](https://gist.github.com/bobbidigital/51704e6ddda8a58c7a9c)

	tell application "Airmail 2"	
	set theMessage to selected message	
	tell theMessage		set theContent to htmlContent		set theSubject to subject	
	end tell	
	tell application "OmniFocus"		tell quick entry			set theRTFMessage to do shell script "echo " & quoted form of theContent & "|/usr/bin/textutil " & " -convert txt -stdin -stdout -format html"			make new inbox task with properties {name:theSubject, note:theRTFMessage}			set note expanded of every tree to true			open		end tell	
	end tell	
	end tell

The script is pretty vanilla, except for the line referencing /usr/bin/textutil. [Textutil](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/textutil.1.html) is an awesome little utility on OS X to convert text from various formats. It's part of the [Cocoa Framework](https://developer.apple.com/technologies/mac/cocoa.html) so it should be available on all Macs running OS X. (Gotta get specific for people that still think Linux is a Desktop OS. OOOOH BUUURRRNNN)

Now you need to make the script useful. 

1. Open [Script Editor](http://www.macosxautomation.com/applescript/firsttutorial/02.html) on your Mac and copy pasta the script into it. Save it some where and make a note of the location.
2. Launch Automator, and choose "Service" as the Document type. 
3. Open a Finder window, and drag your workflow onto the Automator build section.
4. In the upper right hand section, change the in "any application" drop down to Airmail2. (You might have to click other and browse for it)
4. Save the Service via File -> Save


Now that you've create the service, you'll want to create a shortcut for it in Airmail. 

Launch System Preferences and go to Shortcuts. Go to App Shortcuts in the left hand bar. Click the "+" icon.

In the Application section, choose Airmail 2. In Menu Title, type the **exact** name of the service you created above. Choose a Keyboard Shortcut for the last field. I personally use CMD+SHIFT+, but YMMV. Choose what works for you.

Voila. Get better emails in your Omnifocus. Now I'm just waiting for everyone to tell me there was an easier way to do this. Because I **CAN'T** be the only one frustrated by this.

