---
layout: post
title: "Using Emacs for Rails development: The perfect setup"
---

Lately, I’ve started digging more and more into Rails, preparing for the start of a Rails powered project. Although there are some IDEs offering decent Rails support(namely NetBeans, Komodo and Aptana Studio) I have always preferred the comfort of Emacs for various reasons. So naturally I embarked on a quest to setup a suitable environment for Rails development in Emacs. After a couple of days of searching and evaluating possible solutions I finally set up a wordy environment. It consists of a couple of components – ruby-mode, ruby-electric, nxhtml-mode and rinari.

As you probably have guessed by now ruby-mode provides support for editing ruby source files. The mode is pretty feature complete and under active development, headed by none other than Matz himself. You can get it from the ruby svn repository. ruby-electric provides auto insertion of closing braces, quotes, ends, etc. It can also the found in the ruby repo. Instructions how to setup both modes can be found here. Although many people recommend adding pabbrev(a mode which provides auto-completion) to the setup, I don’t recommend it – I find the mode mostly annoying and stick to the old school dumb auto-completion with M-/ .

nxhtml-mode is a pretty comprehensive package for web development in general. We need it for its excellent support for erubis templates(.rhtml, .erb.html) and of course xhtml and css.

rinari is a mode for Rails development – it contains rich functionality such as the ability to easily navigate between models, views and controllers in a Rails application amongst other features. Instructions how to set up rinari together with nxhtml-mode can be found on rinari’s home page.

It’s always a good idea to add ecb(the Emacs code browser) to the mix, though this is entirely optional.

I hope you enjoy this setup and it helps boost your Rails productivity in Emacs
