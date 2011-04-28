---
layout: post
title: "One shell to rule them all..."
---

I've been using zsh for about three years now and continue to be
impressed the its immense power and flexibility. Switching from bash
to zsh was a decision as good as switching from Windows to GNU/Linux,
from vim to Emacs, from Eclipse to IntelliJ IDEA. In other words - it
was an extremely good decision. :-)

So I want to finally get the word out, showcase some nice zsh features
and probably persuade a couple of bash users to try it. Be warned,
however - after you try it there is no going back...

## Getting started

Most distros come with bash by default so you'll probably need to
install zsh first and configure it as your user's shell. On Fedora
you'd do:

{% highlight console %}
[bozhidar@bozhidar ~]$ sudo yum install zsh
{% endhighlight %}

The edit /etc/password and set there zsh as your shell:

bozhidar:x:500:500:Bozhidar Batsov:/home/bozhidar:/bin/zsh

The next time you login a terminal wizard with start up asking you
about some basic zsh options that you might want to enable. I suggest
you to enable them all except the beep option. In the end the wizard
will save the new configuration to the file .zshrc in your user's home
folder.

Alternatively you may just use a preconfigured .zshrc, like this one:

{% highlight bash %}
# Lines configured by zsh-newuser-install
HISTFILE=~/.histfile
HISTSIZE=1000
SAVEHIST=1000
setopt appendhistory autocd extendedglob nomatch notify correct_all
unsetopt beep
bindkey -e
# End of lines configured by zsh-newuser-install
# The following lines were added by compinstall
zstyle :compinstall filename '/home/bozhidar/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall
{% endhighlight %}

I don't like very much the default zsh prompt and I generally change
it right away. Have a look at my other
[short article](/2008/07/27/zsh-prompt.html) on the topic.

## Playing around

At this point you have the legendary zsh autocompletion configured and
you have enabled many of the zsh core features.

* autocd allows you to navigate to folders only with their name
  without the cd command. One of my favourite features. Now you can do
  things like
  
[bozhidar@bozhidar ~]$ Downloads   
[bozhidar@bozhidar ~/Downloads]$

Instead of 

[bozhidar@bozhidar ~]$ cd Downloads   
[bozhidar@bozhidar ~/Downloads]$

autocd was added in bash 4.0 as well. You can enable it there with 

[bozhidar@bozhidar ~]$ shopt -s autocd

* appendhistory all your open shells share the same history which is
  handy if you want to refer commands from one shell in another with
  say Ctrl+R(reverse-history-search)
  
* extendedglob allows you to recursive look for files in folders

[bozhidar@bozhidar ~]$ ls somedir/**/Makefile

is equivalent to 

[bozhidar@bozhidar ~]$ find somedir -name Makefile

Most zsh users never use find for simple file look up. This feature
was also added to bash 4.0 but it works in a slightly different
manner.

$ shopt -s extglob

* correct - autocorrects mistyped commands

[bozhidar@bozhidar]$ cta ~/.zshrc 
zsh: correct 'cta' to 'cat' [nyae]?

# Keybindings 

By default zsh uses Emacs keybindings which is perfect for a long time
Emacs user like me. zsh doesn't use readline, instead it has its own
line editing library called zle, which is much more powerful. vi users
are not forgotten and can switch zsh to vi keybindings with the
command

bindkey -v

Mind that by default you'll be in "insert" mode and have to press ESC
to go into command mode.


