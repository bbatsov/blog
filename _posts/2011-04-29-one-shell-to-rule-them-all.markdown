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

There a couple of configuration files related to zsh that you should
know about:

* .zshrc - runs for each new shell(roughly equivalent to .bashrc)
* .zprofile - runs only for login shells(like .bash_profile)
* .zlogout - runs on logout
* .zshenv - holds environmental variables

Here's an example .zshenv file:

{% highlight bash %}
export JAVA_HOME=/usr/java/latest

export SCALA_HOME=/opt/scala-2.8.1.final

export M2_HOME=/opt/apache-maven-3.0.2

export EDITOR="emacsclient -t"
export ALTERNATE_EDITOR=""

#needed to properly display complex color-themes in Emacs and vim
export TERM=xterm-256color

typeset -U path
path=($M2_HOME/bin $SCALA_HOME/bin ~/bin ~/Projects/work/bin $path)
{% endhighlight %}

Please note the way in which the PATH variable is set in zsh, which
differs substantially from bash(it's just exported there as any other variable).

## Playing around

At this point you have the legendary zsh autocompletion configured and
you have enabled many of the zsh core features.

**autocd** allows you to navigate to folders only with their name
without the cd command. One of my favourite features. Now you can do
things like:

{% highlight console %}  
[bozhidar@bozhidar ~]$ Downloads   
[bozhidar@bozhidar ~/Downloads]$
{% endhighlight %}

Instead of:

{% highlight console %}
[bozhidar@bozhidar ~]$ cd Downloads   
[bozhidar@bozhidar ~/Downloads]$
{% endhighlight %}

By the way autocd was added in bash 4.0 as well. You can enable it there with:

{% highlight console %}
[bozhidar@bozhidar ~]$ shopt -s autocd
{% endhighlight %}

**appendhistory** all your open shells share the same history which is
handy if you want to refer commands from one shell in another with
say Ctrl+R(reverse-history-search)
  
**extendedglob** allows you to recursive look for files in folders:

{% highlight console %}
[bozhidar@bozhidar ~]$ ls somedir/**/Makefile
{% endhighlight %}

is equivalent to:

{% highlight console %}
[bozhidar@bozhidar ~]$ find somedir -name Makefile
{% endhighlight %}

Most zsh users never use find for simple file look up. This feature
was also added to bash 4.0 but it works in a slightly different
manner.

{% highlight console %}
$ shopt -s extglob
{% endhighlight %}

**correct** - autocorrects mistyped commands

{% highlight console %}
[bozhidar@bozhidar]$ cta ~/.zshrc 
zsh: correct 'cta' to 'cat' [nyae]?
{% endhighlight %}

# Keybindings 

By default zsh uses Emacs keybindings which is perfect for a long time
Emacs user like me. zsh doesn't use readline, instead it has its own
line editing library called zle, which is much more powerful. vi users
are not forgotten and can switch zsh to vi keybindings with the
command:

{% highlight console %}
bindkey -v
{% endhighlight %}

Mind that by default you'll be in "insert" mode and have to press ESC
to go into command mode.

You can also create custom keybindings like this:

{% highlight console %}
bindkey '^[[H' beginning-of-line
bindkey '^[[F' end-of-line
{% endhighlight %}

This will bind the Home and End keys to the commands beginning-of-line and end-of-line.
# Aliases

Zsh has three different kinds of shell aliases.

**Regular** - same as in bash:

{% highlight console %}
alias ll='ls -l'
{% endhighlight %}

**Suffix** - suffix aliases are supported in zsh since version
4.2.0. Some examples:

{% highlight console %}
alias -s tex=emacs
alias -s html=google-chrome
{% endhighlight %}

Now when you type in the console

{% highlight console %}
$ somefile.tex
{% endhighlight %}

it will be opened automatically with Emacs. Similarly somefile.html
would be opened by google-chrome. As you might imagine this feature is
quite handy.

**Global** - global aliases can be used anywhere in the command line(as
opposed to regular aliases that can used only in the beginning). Example:
  
{% highlight console %}
alias -g ...='../..'
cd ...  
{% endhighlight %}

# Some tips and tricks

* press Alt+q in the middle of a command you're typing. This will clear 
the console prompt and allow you execute another command(like a man lookup). Afterwards 
the things you've typed before the Alt+q will magically reappear.

* Imagine you're in the folder **project/4.0/module**. Typing:

{% highlight console %}
cd 4.0 5.0 
{% endhighlight %}

Will take you to a folder named project/5.0/module(assuming that it exists of course). In general
the command has the format `cd old new`.

# Conclusion

There is no easy way to sum up everything that makes zsh great in a single blog post. I'll try to
expand and improve it in time. I hope I've whetted your appetite to try out zsh. If you like it
well enough(of which I'm most certain you should have a look at the resources in the end as well).

# Useful resources
* [zsh reference card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)
* [zsh manual](http://zsh.sourceforge.net/Doc/zsh_a4.pdf)
* ["A User's Guide to Z-Shell"](http://zsh.sourceforge.net/Guide/zshguide.html)
* [zsh wiki](http://zshwiki.org/home/)  
* [zsh lovers](http://grml.org/zsh/zsh-lovers.html) - collection of
  tips and tricks
* ["From Bash to Z Shell - Conquering the Command Line"](http://www.bash2zsh.com/)
