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

# Scala at a glance

_If I were to pick a language to use today other than Java, it would
be Scala..._ - James Gosling, creator of Java

_If Java programmers want to use features that aren't present in the
language, I think they're probably best off using another language
that targets the JVM, such a Scala and Groovy._ - Joshua Bloch, author
of "Effective Java" and many of Java's core libraries

Scala basically is:

* SCAlable Language
* Pure OO language
* Functional language
* Statically typed language
* A language that integrates seamlessly with existing Java code
* A great community

Scala's more prominent features are:

* Type inference
* Advanced type system
* Improved OO model
* Improved imports system
* Simplified visibility rules
* Suitable for scripting, GUI, enterprise
* Relies on immutable data structures by default

# Static vs Dynamic typing

# A whirlwind tour of Scala

* Scala is expressive

{% highlight scala %}
scala> val romanToArabic = Map("I" -> 1, "II" -> 2, "III" -> 3, "IV" -> 4, "V" -> 5)
romanToArabic: scala.collection.immutable.Map[java.lang.String,Int] = Map((II,2), (IV,4), (I,1), (V,5), (III,3))

scala> romanToArabic("I")
res2: Int = 1

scala> romanToArabic("II")
res3: Int = 2
{% endhighlight %}

* Scala removes the incidental complexity and cut right to the core of
  the problem. Imagine that you want to find whether or not a string
  contains uppercase characters. In Java you'd write something like this:
  
{% highlight java %}
public boolean hasUpperCase(String word) {
    if (word == null) {
        return false;
    }
    int len = word.length();
    for (int i = 0; i < len; i++) {
        if (Character.isUpperCase(word.charAt(i))) {
            return true;
        }
    }
    return false;
}
{% endhighlight %}

So much boilerplate code (loop, if) to express such a basic idea. In
Scala you'd simply write:

{% highlight scala %}
def hasUppercase(word: String): Boolean = {
  if (word != null) 
    word.exists(c => c.isUpperCase) 
  else 
    false
}

// or more compactly 
def hasUppercase(word: String) = if (word != null) word.exists(_.isUpperCase) else false
{% endhighlight %}

* Scala is concise

Consider this simple JavaBean (well, not exactly JavaBean to be
precise - it lacks a no param constructor) definition:

{% highlight java %}
class Person {
    private String name;
    private int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
{% endhighlight %}

In Scala the equivalent definition looks like this:

{% highlight scala %}
class Person(var name: String, var age: Int)
{% endhighlight %}

This is what I call a good signal-to-noise ratio.

* Scala is pure OO language - everything is an object, operators are
  actually methods, everything yields some result(even constructs such
  as if), there are no static field and methods 
  
* Scala is power overwhelming

{% highlight scala %}
import scala.actors.Actor._

case class Add(x: Int, y: Int)
case class Sub(x: Int, y: Int)

val mathService = actor {
  loop {
    receive {
      case Add(x, y) => reply(x + y)
      case Sub(x, y) => reply(x - y)
    }
  }
}

mathService !? Add(1, 3) // returns 4
mathService !? Sub(5, 2) // returns 3
{% endhighlight %}

# Playing around 

A good way to start exploring Scala is the REPL. Fire it up and type
along:

{% highlight scala %}
scala> println("Hello, Scala")
Hello, Scala
{% endhighlight %}

# Object orientation purification

* Everything is an object
* No operators, just methods
    * 1 + 2 === 1.+(2)
* No static fields & methods - replaced by companion objects

* Traits - the evolution of interfaces
    * Traits are interfaces on steroids
    * They can contain state as well as behaviour
    * Think of them more as Ruby's mixins than Java's interfaces 
    * They can be implemented on the fly by objects
    * They are too complex to be properly explained in one short blog post :-)

# Functional programming

Functional programming has many aspects, but to get the bulk of it you
need just two magical ingredients - support for functions as objects
and a nice array of immutable data structures. Scala, naturally, has
both. Traditionally OOP languages have rarely had much support for
functional programming, which makes it awkward to express some
problems in them. Steve Yegge wrote an excellent article on the
subject some time ago - "Execution in the kingdom of the
nouns"(http://steve-yegge.blogspot.com/2006/03/execution-in-kingdom-of-nouns.html).

**Return of the verbs**

* Functions are first class objects
    * val inc = (x: Int) => x + 1
    * inc(1) // => 2

* Higher-order functions
    * List(1, 2, 3).map((x: Int) => x + 1) // => List(2, 3, 4)

* Sugared functions
    * List(1, 2, 3).map(x => x + 1)
    * List(1, 2, 3).map(_ + 1)
    
**Closures**

Closures are basically functions that have captured variable from an
external scope (variables that were not parameters of the
functions). Closures are often used as the parameters of higher-order
functions (functions that take functions as parameters):

{% highlight scala %}
scala> var x = 10
x: Int = 10

scala> val addToX = (y: Int) => x + y
addToX: (Int) => Int = <function1>

scala> addToX(2)
res0: Int = 12

scala> addToX(6)
res1: Int = 16

scala> x = 5    
x: Int = 5

scala> addToX(10)
res2: Int = 15
{% endhighlight %}

**Functional data structures**

Functional programming revolves around the concept of immutability -
nothing is ever changed - we have some input, we get some output and
the input is not changed in the process. Consider a simple operation
like an addition of an element to a list:

* the operation could modify the list to which the element is being
  added
* the operation can return a new list that is the same as the
  original, but has the additional element
  
Functional programming favours the second approach and Scala as a
functional programming language provides data structures with the
desired behaviour. 

* List - think here of Lisp lists and not Java lists(unless you're
  thinking of Java linked lists that is)
* Maps
* Sets
* Trees
* Stacks

Scala doesn't force you into functional programming, though. Apart
from the List, which is always immutable, we have two types of all the
core data structures mentioned - immutable and mutable. The immutable
data structures are those imported by default to promote a more
functional programming style, but you can easily switch to the mutable
versions and program in an imperative manner.

**List almighty**

The list is a core data structure in functional programming because it
recursively defined and therefore it's very suitable for use in
recursive algorithms. A list is composed of cons cells, each having
two components - the value it holds and a reference to a next cons
cell. The last cell points to a special value - Nil (which happens to
represent an empty list).

1 | -> 2 | -> 3 | -> Nil

{% highlight scala %}
scala> 1 :: 2 :: 3 :: 4 :: 5 :: Nil
res3: List[Int] = List(1, 2, 3, 4, 5)

scala> val names = List("Neo", "Trinity", "Morpheus", "Tank", "Dozer")
names: List[java.lang.String] = List(Neo, Trinity, Morpheus, Tank, Dozer)

scala> names.length
res4: Int = 5

scala> names.foreach(println)
Neo
Trinity
Morpheus
Tank
Dozer

scala> names.map(_.toUpperCase)
res6: List[java.lang.String] = List(NEO, TRINITY, MORPHEUS, TANK, DOZER)

scala> names.forall(_.length > 5)
res7: Boolean = false

scala> names.forall(_.length > 2)
res8: Boolean = true

scala> names.filter(_.startsWith("T"))
res9: List[java.lang.String] = List(Trinity, Tank)

scala> names.exists(_.length == 3)
res10: Boolean = true

scala> names.drop(2)
res11: List[java.lang.String] = List(Morpheus, Tank, Dozer)

scala> names.reverse
res12: List[java.lang.String] = List(Dozer, Tank, Morpheus, Trinity, Neo)

scala> names.sortBy(_.length)
res13: List[java.lang.String] = List(Neo, Tank, Dozer, Trinity, Morpheus)

scala> names.sort(_ > _)
res14: List[java.lang.String] = List(Trinity, Tank, Neo, Morpheus, Dozer)

scala> names.slice(2, 4)
res16: List[java.lang.String] = List(Morpheus, Tank)
{% endhighlight %}

**Pattern matching**

You can think of Scala's pattern matching as a super charged version
of switch, capable of matching on a variety of criteria and of
destructuring that matched objects. Here's a simple example:

{% highlight scala %}
scala> def testMatching(something: Any) = something match {
     |   case 1 => "one"
     |   case "two" => 2
     |   case x: Int => "an integer number"
     |   case x: String => "some string"
     |   case <xmltag>{content}</xmltag> => content
     |   case head :: tail => head
     |   case _ => "something else entirely"
     | }
testMatching: (something: Any)Any

scala> testMatching(1)
res18: Any = one

scala> testMatching("two")
res19: Any = 2

scala> testMatching(2)    
res20: Any = an integer number

scala> testMatching("matrix")
res21: Any = some string

scala> testMatching(<xmltag>this is in the tag</xmltag>)
res22: Any = this is in the tag

scala> testMatching(List(1, 2, 3))                      
res23: Any = 1

scala> testMatching(3.9)          
res24: Any = something else entirely
{% endhighlight %}

# Parallel programming

With the advent of multi-core processors concurrent programming is
becoming indispensable. Scala's primary concurrency construct is
actors. Actors are basically concurrent processes that communicate by
exchanging messages. Actors can also be seen as a form of active
objects where invoking a method corresponds to sending a
message. Actors are not a new idea - Scala's actor library draws heavy
inspiration from Erlang - a programming language notable for its
support for the development of distributed highly parallel systems.

The Scala Actors library provides both asynchronous and synchronous
message sends (the latter are implemented by exchanging several
asynchronous messages). Moreover, actors may communicate using futures
where requests are handled asynchronously, but return a representation
(the future) that allows to await the reply.

Our first example consists of two actors that exchange a bunch of
messages and then terminate. The first actor sends "ping" messages to
the second actor, which in turn sends "pong" messages back (for each
received "ping" message one "pong" message).

We start off by defining the messages that are sent and received by
our actors. In this case, we can use singleton objects (in more
advanced programs, messages are usually parameterized). Since we want
to use pattern matching, each message is a case object:

The ping actor starts the message exchange by sending a Ping message
to the pong actor. The Pong message is the response from the pong
actor. When the ping actor has sent a certain number of Ping messages,
it sends a Stop message to the pong actor.

# Tools

We all know that even the best programming language can be rendered
useless by the lack of good development tools for it - powerful text
editors, integrated development environments, profilers, build tools,
etc. Scala is a relatively young programming language that became
really popular just recently and as a result there are still no
development environments for Scala as powerful as those for Java
(although since both languages use static typing eventually the
environments will be on par). Most popular Java IDEs features feature
some form of Scala support and most Java build tools as well.

* IDE
    * [IntelliJ IDEA](http://www.jetbrains.com/idea/) - the ultimate
      Scala IDE at the moment. It works quite well, but it's a bit
      buggy that the moment (which is to be expected of something with
      some many beta features).

    * [Eclipse](http://www.scala-ide.org/) - the most
      popular Java IDE has a Scala plug-in that
      until recently was mostly useless, but currently is being
      totally reworked and the next stable version will bring usable
      Scala support to the Eclipse users. The development of the new
      Scala plug-in is headed by none other than Martin Odersky himself.

    * [NetBeans](http://wiki.netbeans.org/Scala69) - Presently the
      Scala support in NetBeans is a bit basic, but it's usable.

    * Emacs ENSIME
    
* Scala distribution
    * scala - A Scala REPL for exploratory programming; it's also the
      Scala "interpreter" and the Scala class runner

    * scalac - the Groovy compiler

    * fsc - fast Scala compiler

    * sbaz - The Scala Bazaar System, sbaz for short, is a packaging
      system developed to automate the task of mainaining a Scala
      installation. The program allows you to easily upgrade your
      installation as soon as a new version is available. You can also
      contribute your own packages, and make them easily available to
      other sbaz users.
    
* Build tools
    * [Apache Maven](http://maven.apache.org)
    * [Apache Buildr](http://buildr.apache.org)
    * [Gradle](http://gradle.org)
    * [SBT](http://code.google.com/p/simple-build-tool/)

# Killer apps

Scala presently doesn't have that many killer apps. Here are the most
prominent: 

* Lift web framework
    * Lazy page loading
    * Parallel rendering
    * Comet & Ajax
    * Wiring
    * Designer friendly templates
    * Wizard
    * Security
    
* Akka

* SBT

# Success stories

* Twitter
* Four square
* LinkedIn
* SAP

# Future prospects

# Comparison to Java

It's only natural that Java developers are interested in how Scala
stacks up to Java:

* Pros
    * Scala is fast, just as fast as Java. Some might wonder why this
      is a feature - they should take a look at the performance of the
      most of the other JVM langs and they'll understand. Granted, all
      of the performance benefits come from the use of static typing
      in Scala, but Scala's code is often as concise as the code
      written in a dynamic language like Ruby or Groovy. 
    * Great Java interoperability
    * Scala removes a lot of the incidental complexity of programming
      and let's you express your thoughts directly in the source code
    * The syntax of Scala is mostly uniform and you can usually easily
      create new abstractions that look like language built-ins.
    * Scala features great support for parallel programming.
    * Runs on both Java and .Net (at least in theory)
* Cons
    * Some aspects of the language are fairly complex like the
      subtyping rules for instance. This will probably scare off some
      people, but I can assure you that this complexity is superficial
      and once you've grasped enough of Scala everything will fall
      into place and seem to you the most natural thing in the world.
    * Calling Scala from Java is not as easy as calling Java from
      Scala.
    * The core API is still subject to constant changes and most new
      Scala version are not backward compatible with the old ones
      (unlike in Java).
    * Scala's community (albeit very friendly and helpful) is current
      tiny compared to Java's. You might not get an assistance from
      the community as quickly as you'd get it for Java related problems.

# Epilogue
