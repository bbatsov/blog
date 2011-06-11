---
layout: post
title: "The Linux desktop experience is killing Linux on the desktop"
categories:
- Linux
- Windows
- Rant
---

**Disclaimer**

_This post is a bona fide rant. It tells how a hardcore Linux user
(me) decided to abandon Linux as a desktop platform and the reasons
behind this decision. It might provoke some controversy, but
I frankly don't care._

# Overture

I'm generally known as one of the biggest supporters of GNU/Linux,
I've taught courses on Linux administration, I've spoken at Linux
conferences and I naturally use Linux as my primary desktop on all my
machines. Well, that last part is not so true anymore. Here the story
begins...

# The background

I've been using GNU/Linux exclusively for 8 years now. I've spent a
lot of time with Fedora, Gentoo and Arch Linux. I use it at home, I
use it at work and along the way I've converted many Windows users to
Linux. I've lived through a lot of driver and software problems
with Linux, hoping that the day would come when it will become a
first-class citizen of the desktop operating systems town. Alas, this
day never came and probably never will.

My patience ended this week and I'll be gradually moving all my
desktop machines back to Windows. What caused me to take such drastic
course of action? I've bought myself a new ThinkPad T520 laptop,
powered by Nvidia's Optimus GPU switching technology - when the GPU
load is low it uses the built-in Sandy Bridge GPU, when it gets higher
- it switches to the discrete NVS 4200M GPU. Needless to say - this
  technology is not supported under Linux, but I was prepared to live
  without it. After all both Intel and Nvidia are known to have decent
  Linux drivers so I was about to try both GPU and select the one with
  the better performance. All I had to do was pick a shiny new
  distribution to power my mobile powerhouse...
  
# The Distribution

I love Fedora - always have, always will. They constantly deliver to
the end users the cutting edge in Linux technologies (both desktop and
server), so it's naturally my distro of choice (I'm quite fond of
cutting edge tech). I installed on the new
laptop the latest Fedora 15 with GNOME 3.0 and here the problems
started. GNOME 3 requires 3d acceleration to work properly - a
reasonable requirement these days, at least on an operating system with
normal video drivers. 

The Intel driver sucked so bad that I got constant screen corruption
and hang-ups. Too bad, because I preferred to use the Intel GPU since
I mostly work on the laptop. The open source Nvidia driver nouveau
doesn't support the NVS 4200, so I was forced to install the
proprietary driver. It ran OK initially, but after some time my system
just started to freeze while waiting for Plymouth (probably after some
kernel update, which I didn't notice). I could have tried the usual
tricks and fixed the problem, but at this point I finally realized how
idiotic it was of me to keep using Linux for a desktop OS after all
the shit I've endured and the time I've wasted dealing with stuff that
should have been "just working". I just want to get some work done, I
don't want to waste my time debugging all kind of crap.

# The Shit I endured

**Non-existing ethernet/wireless drivers** - not so common today, but
  try remembering the time circa 2005

**Non-existing/crappy audio drivers** - got an X-Fi 5 years ago, ALSA
  driver was released 3-4 years later and was total piece of garbage,
  OSS driver was barely usable

**Lamest video card drivers ever** - most video card drivers for Linux
  are so bad I cannot even watch tear-free video. Nvidia have the only
  decent video driver, but it's far from perfect either - no KMS, poor
  2D acceleration. AMD's drivers are a punishment from the Lord and
  Intel's constantly "evolving" drivers are barely usable most of the
  time. The video card drivers made me buy and HD media player and an
  PS3 (for which I'm thankful), but I have to ask myself - why suffer
  all this shit instead of getting a normal desktop OS like OS X or
  Windows? Did I love Linux that much? Did I believe that much it's
  desktop day would come? What an idiot I was.

**Lack of printer drivers** - that's a funny one. Often printers
  listed as having Linux drivers are mostly unusable. The printer that
  own is listed as having a "perfect" Linux compatability in
  openprinting.org. If this is perfect I cannot begin to imagine what
  is "poor" compatibility.
  
**Crappiest suspend/resume support** - laptop goes to sleep, but
  doesn't wake up. Wireless dies after wake up. Suspend/resume used to
  be something mythical to most Linux users. Recently the situation
  has improved a bit it's still light years away from what you get
  with Windows/OSX.

I'll stop writing about the driver problems now, because they affect
so many thing. Even my fairly advanced mouse is missing some functions
in Linux. I'm not even mentioning the things like support for "Turbo
Memory", Optimus, etc.

**Lack of decent office software** - call it OpenOffice.org and don't
  insult it anymore...
  
**Problematic sound architecture** - let me be completely blunt -
  everything sound related in Linux sucks - OSS, ALSA, PulseAudio (the
  sucker king). From a technical standpoint OSS never actually sucked,
  but since it wasn't picked up by the community the project fell
  into oblivion. How many of you have enjoy Dolby Digital or DTS sound
  from their Linux boxes? 
  
**Poor flash support** - should I explain? Have you tried it on a 64
  bit distro? Do I hate it? Sure. Do I hope HTML5 will kill it?
  Sure. Do I need it? Sure.
  
**Poor skype support** - Same story as with flash. I keep dreaming of
  a world with more intelligent users where GTalk has a conference
  mode and everybody's using it instead of skype.
  
**Poor quality of desktop apps** - Known issues in core applications
  such as Nautilus don't get fixed for years. Such things naturally
  piss me off. Trying to contribute to the solution of a problem is
  often met with apathy by maintainers. Btw Linux users thing that
  Mozilla Firefox is very slow and memory hungry - but it turns out
  that the Windows version is generally performing a lot better (not
  to mention - supporting hardware video acceleration).

I can keep listing things here forever. When I come to think about it
for the entire time I've been using Linux only one major problem got
resolved - USB devices support. I still remember the days when I had
to write auto mounting policies myself or to use _mount_ manually all
the time. I won't even mention the quality of most proprietary apps on
Linux, the huge amount of missing essential application and the
unavailability of mainstream video games.

So this is it! Asta la vista, Linux! You still remain the best server
operating system, though. You'll always have a special place in my
heart and a VMWare instance on my Windows boxes. 

# What I'll miss

- shell
- transparency
- package management

Although most common desktop users probably don't use the shell very
often, I practically live(d) in it. OS X has zsh and bash, so it's a
long term option for me, but due to the need for new hardware I'll be
using Windows 7 on the desktop front for now. Hopefully the rumors
that PowerShell is great will turned out to be true.

The ability to tweak every aspect of the configuration, to build
custom drivers and kernels will be missed as well, but I don't tend to
do this as often as I used to. 

Probably the biggest loss for me would be the wonderful distro package
management systems like YUM and APT.

# Epilogue

I remember the first time I used Linux. A friend of mine installed
Fedora 2 on my personal computer and there was a glitch in GRUB that
prevented me from booting in Windows. My ethernet card wasn't
supported so I was left without Internet. I asked my friend can I at
least watch a few movies while he brought me a patched version of the
buggy GRUB. He told me - you need to compile MPlayer from sources with
several optimization, you need windows video codecs, etc. At the time this
excited me a lot - adventure, excitement. I learned A LOT by using
Linux non-stop for so long time. But at some point you stop learning
exciting things and are just stuck with tedious things you have to
keep doing over and over again. And as I already mentioned - I don't
want my time wasted, I want to get the job done with minimum hassle.

I've been hearing each and every year that "year 20xx" will be the
year of the Linux desktop. It never came and it's my firm believe that
it never will. Constantly plagued by hardware and software woes Linux
is doomed to fail. Without major support from hardware and software
vendors every OS is ultimately doomed to fail. 

It's no secret that a lot of money are made by Linux server businesses
and this naturally drives a lot of the development in the area of
improving server performance. Nobody put it better than
[Con Colivas](http://apcmag.com/why_i_quit_kernel_developer_con_kolivas.htm)
- "_Linux is burdened with enterprise crap that makes it run poorly on
  desktop PCs, says kernel developer Con Kolivas who recently walked
  away from years of work on it._". Linux will remain the king of the
  server world, but on the desktop front it will always be an OS for
  enthusiast and hackers only.
  
Goodbye, my dear old friend. You'll be missed... but not that much.

P.S. Btw I'm as pro a Linux user as they get - a professional sys
admin, a former kernel developer so don't bother me with moronic
comments from the type "you're not doing something right/you should
try another distro".
