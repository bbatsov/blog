---
layout: post
title: Emacs configuration in github
---

When you have applications, whose configuration is as complex as that
of Emacs it’s always a good idea to store that configuration under
version control so you can easily share it between multiple
computers. You can always set up some version control system yourself,
but it’s a lot more convenient(and much more reliable) to use an
already existing code hosting solution such a GitHub. I have created a
small repo there housing my humble Emacs configuration(.emacs, some
custom stuff) and share it on all the computers that I work. You may
have a look at my Emacs repo here.

In case you’re wondering why there is no file named .emacs in there – my .emacs actually consists of only one line:

(load “~/emacs/dot-emacs.el”)
