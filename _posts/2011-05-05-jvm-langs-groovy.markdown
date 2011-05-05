---
layout: post
title: "JVM Languages Week - Day 1 - The Groovy Programming Language"
---

In a series of articles labelled commonly "JVM Languages Week" I'll
discussing modern alternatives to the Java programming language. This
is the first instalment of the series - "The Groovy Programming
Language".

# Overture

We all know and love the Java _platform_(note the emphasis on
platform) for a couple of obvious reasons. Most notably it features a
huge high quality standard library and a legendary execution
environment - the Java Virtual Machine(JVM). The JVM is known to
posses the following qualities:

* Runs on all major platforms
* Enterprise ready
* Extremely stable
* Extremely fast
* Highly customisable - many aspects of its work can easily be
  adjusted such as GC settings, heap settings, etc.

There is a terrific community around the Java platform that has
contributed an immense amount of high quality software vital to the
success of Java. Hibernate, Spring, Eclipse, NetBeans, the myriad of
Apache projects are all community efforts.

So far so good, but it's not all rainbows and unicorns in the land of
Java. The Java programming language is a common source of gripe
amongst many developers for various reasons. I'll list here some of
the more notable of them:

* It's not a pure OOP language(there is a difference between primitive
  and reference data types)
* It uses static typing(highly subjective topic, but commonly brought up)
* It doesn't have support for closures(which instantly kills half of
  functional's programming ideas such as higher order functions)
* It has limited meta programming capabilities(compared to Ruby and
  Lisp for instance)
* There is no concept of top-level procedures(outside of class
  definitions)(this makes Java unsuitable for creating "script" programs)
* Its syntax is too verbose
* It's not suitable for the creation of DSL
* Its development is sluggish and restrained by the corporate promise of backward compatibility 
* It's an imperative language
* It's parallel programming model is revolving mostly around locks and
  threads
  
Naturally there are some languages that alleviate some(most) of Java's
problems such as:

* Ruby
* Python
* Lisp
* Erlang
* Haskell

They all, however, lack(by default) an execution environment that can
match the JVM. They also lack Java's immense amount of libraries
currently available. When enthusiasts started porting existing
languages to the JVM this came as no surprise - it was only
logical. For instance some folks ported Ruby to Java which resulted in
JRuby, Python also got a Java port called Jython. Though a lot of good
has come from such ports they was also a price to pay. In the case of
Ruby and Python some libraries are not written in Ruby/Python, but in
C for performance reasons, which naturally leads to problems when you
factor in a Java implementation of the language. There is also the
fact that the JVM(currently) doesn't have support for dynamic memory
dispatching which is feature vital for dynamically typed languages to
get a decent performance. For this reason Jython is notoriously
slow. The JRuby team did a much better work, circumvented a lot of the
JVM limitations and actually managed to create a Ruby implementation
that in some scenarios beats the performance of the standard MRI Ruby
1.9 with it's custom YARV virtual machine implemented in C. JRuby will
be the object of a further discussion down the road. 

I'd like to lead this discussion in another direction, however -
programming languages that were implemented from scratch with the JVM
as their execution environment. While there are many of those three
stand out and have gathered a significant momentum in recent
years. They will be the subject of this post and the following
two. Without further adieu I'd like you to meet Groovy, Scala and
Clojure.

We'll begin our discussion with Groovy...

# Meet Groovy

_"Groovy is like a super version of Java. It can leverage Java's
enterprise capabilities but also has cool productivity features like
closures, builders and dynamic typing. If you are a developer, tester
or script guru, you have to love Groovy."_ - praise for Groovy from
<http://groovy.codehaus.org/>

Groovy is:

* is one of the two standard languages for the JVM(the other is Java
of course)
* is an agile and dynamic language for the Java Virtual Machine
* builds upon the strengths of Java but has additional power features inspired by languages like Python, Ruby and Smalltalk
* makes modern programming features available to Java developers with almost-zero learning curve
* supports Domain-Specific Languages and other compact syntax so your
  code becomes easy to read and maintain 
* makes writing shell and build scripts easy with its powerful processing primitives, OO abilities and an Ant DSL
* increases developer productivity by reducing scaffolding code when developing web, GUI, database or console applications
* simplifies testing by supporting unit testing and mocking out-of-the-box
* seamlessly integrates with all existing Java classes and libraries
* compiles straight to Java bytecode so you can use it anywhere you
  can use Java
  
Some of Groovy's most compelling features are:

* Pure OOP language
* Mostly Java compatible syntax
* Optional typing
* No need to wait for Java 7/8/9
    * Closures
    * Attributes
* Duck typing
* BigInteger based arithmetic
* SQL, XML & Swing improvements

A core idea guiding the design of Groovy is make it easy to use for
existing Java developers. Groovy's designers have gone for far in that
direction that the Groovy compiler will happily compile most Java
source files without the need for any modifications. Groovy, however,
builds heavily upon the standard Java's syntax and you'll do well to
get a grip of Groovy's core idioms. Groovy's syntax in a nutshell:

{% highlight groovy %}
// old school Java code, but also valid Groovy code
System.out.println("Hello, world!");

// idiomatic Groovy
println "Hello, world!"

// dynamic variable definition
def name = "Bozhidar"

// GString featuring string interpolation
println "Hello, $name"  // => "Hello, Bozhidar"

// statically typed variable
String songName = "Coding in the Name of"

println "Now playing - $songName"

String multiline = """this is a multiline
string. There is not need to embed
newline characters in it"""

println multiline

// method definition
def greet(name) {
    println "Hello, $name!"
}

// method invocation
greet "Bozhidar"
greet("Bozhidar")

// safe dereferencing
def showSize(list) {
    println "List size is: ${list?.size}"
}

showSize([1, 2, 3])
// this is the important part
showSize(null)

// a list
def beers = ["Zagorka", "Bolyarka", "Shumensko", "Ariana"]

beers.each { beer -> println beer }

// imports can appear anywhere and support the creation of aliases
import static java.util.Calendar.getInstance as now
import java.sql.Date as SDate

println now()
// java.util package is automatically imported in Groovy so this is java.util.Date
println new Date()
println new SDate(2011, 5, 5)

// language support for regular expressions
if ("Hello, Groovy" =~ /\w+,\s\w+/) {
    println "It matches"
}

// range filtering with higher-order functions
(1..10).findAll { n -> n % 2 == 0}.each { n -> println n }

// map
def capitols = [Bulgaria: "Sofia", USA: "Washington", England:"London", France:"Paris"]

println capitols["Bulgaria"] // => Sofia
println capitols["France"]  // => Paris

// class definition
class Person {
    def name
    def age

    Person(name, age) {
        this.name = name
        this.age = age
    }

    @Override
    String toString() {
        return "Name {$name}, age {$age}"
    }
}

def me = new Person("Bozhidar", 26)
println me
{% endhighlight %}

Like Ruby and Python Groovy has language support for commonly used
data structures such as lists, maps, ranges and regular expressions:

* List - def number = [1, 2, 3]
* Map - def countries = [BG: “Bulgaria”, DE: “Germany]
* Range - def range = 1..1000 
* Regular expressions - def whitespace = /\s+/

Groovy comes with its very own standard library(GDK) which builds upon
the JDK(for instance the File and String classes are enhanced in
Groovy) and offer some new features like the Groovy's famous builders.

# OOP in Groovy

* Similar capabilities to Java
    Define classes, interfaces, enums, annotations

* Differences to Java
    Classes (and interfaces etc.) public by default
    Methods public by default
    Property support within classes (auto-setters/getters)
    Duck typing


# Data access handling

Groovy offers some nice improvements over JDBC and JAXP for handling
database queries and XML parsing.

{% highlight groovy %}
import groovy.sql.Sql

}
{% endhighlight %}

{% highlight xml %}
<records>
<car name='HSV Maloo' make='Holden' year='2006'>
<country>Australia</country>
<record type='speed'>Production Pickup Truck with speed of 271kph</record>
</car>
<car name='P50' make='Peel' year='1962'>
<country>Isle of Man</country>
<record type='size'>Smallest Street-Legal Car at 99cm wide and 59 kg weight</record>
</car>
<car name='Royale' make='Bugatti' year='1931'>
<country>France</country>
<record type='price'>Most Valuable Car at $15 million</record>
</car>
</records>
{% endhighlight %}

{% highlight groovy %}
def records = new XmlParser().parse("records.xml")
records.car.each {
println "year = ${it.@year}"
}
{% endhighlight %}

# Builders

{% highlight groovy %}
import groovy.xml.*
def page = new MarkupBuilder()
page.html {
head { title 'Hello' }
body {
ul {
for (count in 1..5) {
li "world $count"
} } } }
{% endhighlight %}

Result:

{% highlight html %}
<html>
<head>
<title>Hello</title>
</head>
<body>
<ul>
<li>world 1</li>
<li>world 2</li>
<li>world 3</li>
<li>world 4</li>
<li>world 5</li>
</ul>
</body>
</html>
{% endhighlight %}

{% highlight groovy %}
import java.awt.FlowLayout
builder = new groovy.swing.SwingBuilder()
langs = ["Groovy", "Ruby", "Python", "Pnuts"]
gui = builder.frame(size: [290, 100],
title: 'Swinging with Groovy!') {
panel(layout: new FlowLayout()) {
panel(layout: new FlowLayout()) {
for (lang in langs) {
checkBox(text: lang)
}
}
button(text: 'Groovy Button', actionPerformed: {
builder.optionPane(message: 'Indubitably Groovy!').
createDialog(null, 'Zen Message').show()
})
button(text: 'Groovy Quit',
actionPerformed: {System.exit(0)})
}
}
gui.show()
{% endhighlight %}

# Groovy tooling

* IDE
	* [IntelliJ IDEA](http://www.jetbrains.com/idea/) - the ultimate
      Groovy IDE. It's excellent Groovy support is part of its open
      source Community Edition.
	* [Eclipse](http://groovy.codehaus.org/Eclipse+Plugin) - the most
      popular Java IDE has an actively maintained Groovy plugin
	* [NetBeans](http://netbeans.org/features/groovy/) - Like IDEA
      NetBeans features built-in Groovy support
    
* Groovy distribution
	* groovysh - A Groovy REPL for exploratory programming
	* groovyconsole
	* groovyc - the Groovy compiler
    
* Build tools
	* [Apache Maven](http://maven.apache.org)
	* [Apache Buildr](http://buildr.apache.org)
	* [Gradle](http://gradle.org)
    
# Killer apps

* [Grails](http://grails.org)
	* Groovy port of Ruby on Rails
	* Leverages the best Java technologies
		* Hibernate
		* Spring
		* Tomcat
* Gradle - powerful build tool
* [Griffon](http://griffon.codehaus.org/) - a Grails like application framework for developing desktop applications

# Groovy resources

* Books
* On-line resources

# Epilogue

Groovy is a language aiming to bring dynamic productivity to Java
developer without introducing them to a steep learning curve. The
language is beautifully architectured and integrates seamlessly with
the existing Java libraries and infrastructure. My biggest gripe with
Groovy is the lack of advanced support for parallel and concurrent
programming. Groovy's performance is not stellar either, but I guess
this will be improved upon in Java 7. 

With its easy to grasp Java-like syntax Groovy is a solid contender
for the attention of Java developers. A growing number of Groovy
related job offerings is a sign of Groovy's acceptance as a industrial
strength tool. 

---
_P.S. Coming up next is a discussion of the Scala programming
language._
