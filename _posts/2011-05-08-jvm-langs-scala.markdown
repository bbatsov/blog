---
layout: post
title: "Java.next() - Scala: The Revenge of the Static Typing"
---

# Overture

This is the second post from my series dedicated to modern programming
languages for the Java platform. Last time we've discussed the
[Groovy programming language](/2011/05/06/jvm-langs-groovy.html) which
is a member of the ever expanding family of dynamic programming
languages. The Scala programming language that is the object of
today's discussion is another beast entirely - not only it uses static
typing(like Java & C#), but it also puts a heavy emphasis on the type
system, functional and parallel programming.

In theory Scala runs both on the JVM and on the CLR(the .NET VM). The
Java port, however, receive a lot more attention by Scala's developer
and it probably accounts for close of to all of Scala's
deployments(especially in production).

# A brief history of Scala

After having written hundreds of thousands lines of Java himself,
Martin Odersky, Professor at EPFL, was well aware of the frustrations
faced by Java programmers. He formed the vision of applying the best
knowledge of the academic research community to the problem of making
the Java programming experience better, even fun. His first pragmatic
step was Java Generics, seen as a major success by the Java
community. But for the full vision of scalable concurrent programming
to be achieved he saw that the basic Java syntax would need to
change. You simply couldn't get there from here. But a deceptively
simple shift in syntax gained better uniformity to the object-oriented
aspects of Java, and this in turn enabled a natural fusion with
functional programming concepts which are critical for tackling
concurrency. In 2001 Scala was born.

Scala stands for a SCAlable LAnguage. What does this mean? Scala is
designed to tackle solutions of wildly varying sizes - from small
scripts (programming in the small) to massive distributed enterprise
applications (generally programming in the large). Scala also means
_steps_ in Italian and this is the reason why most Scala books have
some form of steps on their covers (arguably this is the reason while
Scala is very popular in Italy and particularly in Milan). 

The current production version of Scala is 2.8.1 with 2.9.0 being in
the release candidate stages.

# Installing Scala

**Universal installer**

Scala has an [universal installer](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final-installer.jar) that could be ran on every platform
with Java installed. You can run it from the console like this:

{% highlight console %}
$ java -jar scala-2.8.1.final-installer.jar
{% endhighlight %}

Alternatively, on most systems simply double clicking the installer
jar will run it(assuming you have a GUI environment and assuming that
the java command is associated with jar files - something that is
usually so by default).

**Installing from binary archive**

Just download the Scala distribution for [Unix, OS X and Cygwin](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final.tgz) or
the one for
[Windows](http://www.scala-lang.org/downloads/distrib/files/scala-2.8.1.final.zip)
and extract it somewhere. I'm a GNU/Linux user and I tend to extract
all third party apps in the /opt folder:

{% highlight console %}
$ sudo tar xf scala-2.8.1.final.tgz -C /opt
{% endhighlight %}

You'd also want to add the folder containing the Scala binaries
(compiler, REPL, etc) to your PATH environmental variable. Unix users
might add something like this to their shell startup script (like
.bashrc):

{% highlight bash %}
export JAVA_HOME=/usr/java/latest
export SCALA_HOME=/opt/scala-2.8.1
export PATH=$SCALA_HOME/bin:$PATH
{% endhighlight %}

You should now have Scala installed properly. You can test this by
typing the following in a command shell:

{% highlight console %}
$ scala
{% endhighlight %}

Which should create an interactive Scala shell where you can type
Scala expressions. 

To run a specific Scala script type:

{% highlight console %}
$ scala SomeScript.scala
{% endhighlight %}

**Linux installation**

Most Linux distributions provide Scala through their integrated
package management system. On Debian(and derivatives like Ubuntu) you
can install it like this:

{% highlight console %}
$ sudo apt-get install scala
{% endhighlight %}

On Red Hat systems the magic incantation looks like this:

{% highlight console %}
$ sudo yum install scala
{% endhighlight %}

Personally I'd prefer the platform-independent installation method,
since some distribution package Scala in a non-standard manner which
confuses IDEs for instance.

# Playing around

A good way to start exploring Scala is the REPL. Fire it up and type along:

# Object orientation purification

# Functional programming

Functional programming has many aspects, but to get the bulk of it you
need just two magical ingredients - support for functions as objects
and a nice array of immutable data structures. Scala, naturally, has
both. 

# Parallel programming

# Tools

# Killer apps

# Success stories

# Future prospects

# Epilogue
