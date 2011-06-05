---
layout: post
title: "Emacs Tip #1: Set the default font in Emacs 23"
categories:
- Emacs
- Linux
---

Emacs 23.2 will pick up the default GNOME monospaced font, so if
you're a GNOME user - you're basically covered. If you're not - don't
worry.

The simplest way to set the Emacs font is just to add the following
in your .emacs (or init.el):

{% highlight cl %}
(set-default-font "Inconsolata-12")
{% endhighlight %}

This code will set the Emacs font to Inconsolata (my favorite
monospaced font) with font size 12pt. The problem with this approach
is that it will not work with a X Emacs client (emacsclient -c)
connecting to an Emacs daemon (emacs --daemon), because the code will
get run when the server starts and will basically mean nothing to
it. You can alleviate this problem by using the appropriate hook for X
clients, but I find this distasteful. A much simpler solution is to
forget about _set-default-font_ altogether and simply create a file
named **.Xdefaults** in your home folder. Put the following in it:

{% highlight console %}
Emacs.font: Inconsolata-12
{% endhighlight %}

Afterwards run the following command:

{% highlight console %}
$ xrdb -merge ~/.Xdefaults
{% endhighlight %}

At this point you can start Emacs (in normal or daemon mode) and
your new font settings should be in effect.
