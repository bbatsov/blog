---
layout: post
title: "The Linux desktop experience is killing Linux on the desktop,
Part II"
categories:
- Linux
- Windows
- Rant
---

**Disclaimer**

_Read this with an open mind._

# Overture

A few days back I wrote a somewhat controversial article
called,
["The Linux desktop experience is killing Linux on the desktop"](//Linux/Windows/Rant/2011/06/11/linux-desktop-experience-killing-linux-on-the-desktop.html). While
many readers seem to have grasped the true purpose of the article, a
lot of people claimed the article was nothing but FUD (a favorite term
of many people in the Linux community that would rather ignore
problems than face/acknowledge them).

If you've read my last post and generally agree with it - don't bother
reading this one. It's basically more of the same - in greater detail
and with less profanities. 

In this article I'll have a look at the state of the Linux desktop,
it's usability, strengths and weaknesses. 

# Let's get some facts straight

I'm writing this post from my Emacs 23.2 client connected to my Emacs
daemon, running on my Fedora 15 GNOME 3.0 desktop at home. This
machine has its every part carefully selected for maximum Linux
compatibility (the machine is a bit old, but that wasn't always the case) -
a GeForce 9600GT known to work "great" with the open-source nouveau
driver, an Asus Xonar DX sound card, supported by the great Oxygen HD
audio driver, etc. I do know how to buy hardware (contrary to popular
belief). Actually I've been a hardware
enthusiast for most of my life and I know much more about the inner
workings of computer components than most people. That said - the hardware that
I bought for my home PC was not the hardware that I wanted to buy, but
the one I had to buy. 

One of the great things about using a free (as in speech) OS like
Linux is that you get to do things exactly the way you want to do
them. You're in control. Everything is transparent. It's sad that this
doesn't extend to the ability to pick any piece of fairly generic
hardware and properly enjoy it.

A reader pointed me to
[this piece](http://blog.eracc.com/2011/06/14/the-century-of-the-linux-desktop/)
- a rebuttal of my article. Here's an excerpt:

_Here we go again. Some fellow has gotten all whiny about being such a
big Linux fan, "… hardcore Linux user …", but he just had to go back
to Microsoft to get things done. Why? Because he is tired of having to
tinker with Fedora Linux to make things work, or fail to work, with
cutting edge hardware … and 64-bit Flash on 64-bit Linux is sucky …
and Skype on Linux is sucky … and … and … and. It was all just so
painful and time consuming he could not take it any longer and went
back to the safe arms of Microsoft to escape the horror that is
Linux. Good grief.
Okay, first and foremost, a true "hardcore Linux user", in my mind a
fan of Linux, is unlikely to switch from Linux to anything else. Oh
yes, he or she will switch Linux distributions in a heartbeat, or
maybe three heartbeats, if a distribution fails to work as needed. But
switching to Microsoft and leaving the Linux desktop behind? Not
likely, my friends. I consider myself a true "hardcore Linux user" and
I see no voluntary switch from Linux in my future … ever._

This bit produced a sad smile on my part. Had to go back to Microsoft?
Absolutely not. Chose to use Windows 7 (for the time
being)... If I was to go back to something it should have been FreeBSD
since it was the OS I was using before Linux (and of course Windows
before that indeed). I actually switched quite reluctantly from
FreeBSD to Linux for a simple reason - Linux supported wider hardware
variety and there were more native apps for it.

All Unix-derived OSes are more or less the same from an user's
perspective - mostly the same environment, the same applications. The only thing that really makes the difference is the
hardware support and Linux is clearly far ahead of its competition. 

Hardcore user? You bet! But hardcore doesn't mean an 'unreasonable
idiot, blinded by zealously'. It's not always that someone's favorite
technologies are the best solution to a problem. The section "the shit
I've endured" had dual purpose list a few problems and show how
resilient I am.

Distro hopping is something that mostly newbies do, because they fail
to grasp a fundamental thing in the land of Linux - 95% of the stuff
that comprises a distribution is generic stuff found in most other
distros. You cannot seriously expect that the same drivers in a
different distro will yield wildly different results... Sure, bug do
tend to occur, and sometimes they are truly distribution specific. 

# The process of driver development

My former post placed a heavy emphasis on existing driver
issues. While I abhor some Linux drivers I've never ever blamed the
authors of open source drivers. Here's why:

The year and a half I've spent writing Linux drivers for a proprietary
Austrian company was some of the hardest time in my professional
career. Writing drivers is fairly hard task for two reasons - you have
to have very intimate knowledge of the hardware at hand and you have
to write very safe code, because otherwise you might bring the whole
kernel down. I was basically reading tech specs (most boring read in
the world) most of the day and
writing very little code in end. Debugging drivers is not a pleasant
task either. 

Linux certainly has some of the best developers in the world. I have
little doubt in that. The problem is that these same developers spent
their days working other jobs and you cannot seriously expect them to
have the time or the energy (not to mention the specs required) to
produce drivers that are on par with commercial counterparts developed
for OSX and Windows by big team with vast resources at their disposal.

This is the actual problem as I see it - we're expecting individuals
to create good drivers for us out the goodness of their hearts in
their little spare time with little or no hardware specs on which to
rely.

I've read the source code of many network layer drivers in the Linux
kernel and I've noticed a common trend - a lot of the drivers were
actually written by hardware engineers (instead of software engineers)
- they are filled with copy/paste segments from other drivers, lots of
  useless/dubious/dangerous code. This doesn't surprise me - few
  software engineers have solid grasp of hardware and/or the will to
  take part in driver development. 
  
The hardware vendors are the only party that deserves blame for the
sorry state of many drivers. I cannot believe how hard it is for a
company with the size of AMD to fail to deliver a decent Linux driver
for so many years. Their driver is a monument of everything that is
wrong with hardware vendors as far as Linux is concerned - no support
for latest kernels/X, no support for current state-of-the-art Linux
technologies, notorious instability and performance.

# The desktop software stack

Is it really better for the users?

The lone wolf problem

# Future

# Epilogue

While I was writing this I got another GNOME 3 shell corruption (time
for killall gnome-shell to take the stage). 
