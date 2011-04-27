---
layout: post
title: "Programming languages worth learning"
---

Programming languages have always been a passion of mine and through
the years I've learnt quite a few of them. The first one was Pascal
some 13 years ago and the last was Scala just a couple of months ago.

Although the authors of many languages claim that the language they
created is the greatest thing after hot water, this is rarely the
case. Most of the "unique" features are not quite unique and the truly
unique stuff is often just useless. I don't believe that there is a
single greatest and unparallelled language, but I do believe that some
languages are more valuable them others in term of both theory(the
concepts around which they revolve) and practice(the chances of you
landing a job with them or simply getting a task done).

In this blog post I've review the ten or so languages that I found to
be most enlightening/helpful to me over the years. I think that every
professional software engineer should have at least a passing
knowledge of them.

#C
---
The C programming language has been around for more than forty years
now. While it's often viewed as a higher level assembly language today
in the era of Java, .Net and Python C remains the sole choice for
doing serious system programming - writing drivers, all kinds of
servers and virtual machines. 

The best way to get started with C
hasn't changed in the past 20+ years - just pick a copy of ["The C
Programming Language"](http://www.amazon.com/Programming-Language-2nd-Brian-Kernighan/dp/0131103628) by K&R.

#Lisp 
--- 
_"Lisp is worth learning for the profound enlightenment
experience you will have when you finally get it; that experience will
make you a better programmer for the rest of your days, even if you
never actually use Lisp itself a lot."_ - Eric Raymond

One of the oldest programming languages around - created in 1958 and
still relevant today. Important for its unique code is data approach,
advanced code generation facilities(macros) and the ability to develop
software in incremental and interactive fashion. Although many of the
features that originally made it truly unique(like garbage collection,
if expression, function objects) are found in many modern languages
Lisp still offers some compelling alternatives for those interested to
explore it. 

You cannot start with a better introduction to Lisp that
Peter Seibel's ["Practical Common Lisp"](http://www.gigamonkeys.com/book/).

#Java
---
Let's face it - if you're in the market for jobs a third of them are
about Java EE or Android development. The language is not quite
elegant, but the platform is truly magnificent. Although there are
many other languages targeting the JVM(Scala, Groovy, Clojure, JRuby,
Jython - just to name a few) Java is still predominant by a wide
margin and this is unlikely to change soon.

I've taught a couple of introductory Java programming courses(in
Bulgarian), but I'd recommend the ["Core Java"](http://www.amazon.com/Core-Java-TM-I--Fundamentals-8th/dp/0132354764/ref=sr_1_1?s=books&ie=UTF8&qid=1303901341&sr=1-1) over my lectures any day of
the week. :-)
#Haskell
---
Functional programming has been gaining popularity in recent years
with the rise of parallel computers and of the pure functional
programming languages Haskell is probably the closest to the
mainstream. It features great ideas like type inference, lazy
evaluation, monads, pattern matching. As with Lisp many of the
features of Haskell can be found in more impure packages(like Scala
and Clojure), but Haskell is still the top pure functional language in
my humble opinion. It also has really great free learning resources
on-line like ["Learn you a Haskell for great good"](http://learnyouahaskell.com/) and ["Real world
Haskell"](http://book.realworldhaskell.org/read/)

#Perl
---
Once the undisputed king of the Internet Perl has recently fallen down
from grace in its battle with the newer generation of dynamic
languages like PHP, Ruby and Python. While I wouldn't advise anyone to
start writing Web apps with Perl it's still the best language for
writing administration and helper scripts with minimum fuss and maximum
developer throughput. It also has the greatest support for text
processing ever and an extremely flexible(albeit a bit of confusing)
syntax. 

Pick up a copy of ["Learning Perl"](http://oreilly.com/catalog/9780596520113) and just browse the excellent
*perldoc* and start coding in Perl right away.

#Clojure
---
Clojure is a Lisp dialect with an unique support for parallel and
concurrent programming and runs on top of the venerable JVM. If you're
looking to do some serious parallel programming look no further.

To get started I recommend you to watch the free Clojure screencasts
on [blip.tv](http://clojure.blip.tv/).

#Prolog
--- 
The most famous language from the logic programming family. Solving a
problem like a sudoku puzzle in Prolog will be an eye opening
experience for any developer. While it's unlikely that you'll ever use
it practice the ideas found in Prolog will truly expand your thinking
horizons.

#Ruby
---
A pure object oriented dynamic scripting language with a very nice support for
metaprogramming. Has versions written in Java(JRuby) and
.Net(IronRuby). The language became popular with the rise of the Ruby
on Rails web framework, but it has many applications that don't
involve RoR or web development. 

["Programming Ruby"](http://www.amazon.com/Programming-Ruby-1-9-Pragmatic-Programmers/dp/1934356085/ref=sr_1_1?s=books&ie=UTF8&qid=1303901367&sr=1-1) and ["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177/ref=sr_1_3?s=books&ie=UTF8&qid=1303901367&sr=1-3) are two of the
best introductory Ruby books around.

#Scala
---
An interesting blend of pure object orientation and functional
programming with some concurrency support baked in(actors). Of the
current crop of JVM languages next to Clojure Scala looks most
promising. It features an advanced static type system(more advanced
than Haskell's), state of the art Java integration, support for
pattern matching, extractors and other functional goodness. If any
language has a chance of displacing the Java programming language it
must be Scala...

Start your journey to Scala mastery with ["Programming in Scala"](http://www.artima.com/pins1ed/).

#Conclusion
---
We cannot be experts in ten or twenty programming languages - I'm
certain of that. I do,
however, believe that all the ideas and techniques that we discover in
different programming languages will generally enrich our thinking and
make us better software engineers in principle.
