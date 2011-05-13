---
layout: post
title: "Java.next() - Clojure: The Return of the Lispers"
categories:
- Clojure
- Java
---

# Overture
 
This is the third part of the series of **Java.next()**. Last time
we've discussed the merits of [Scala](http://batsov.com/2011/05/08/jvm-langs-scala.html) - an OO language with a strong
emphasis on functional and parallel programming. Today we'll be
discussing Clojure - a language that pushes the envelop a lot further
than Scala as far as functional and parallel programming are
concerned. You'll see that Clojure is radically different from Scala
and Groovy in many aspects - it's not an OO language, it doesn't have
Algol-derived syntax and it introduces a few rather radical ideas on
subjects such as identity and state.

Clojure's approach to concurrency is characterized by the concept of
identities, which represent a series of immutable states over
time. Since states are immutable values, any number of workers can
operate on them in parallel, and concurrency becomes a question of
managing changes from one state to another. For this purpose, Clojure
provides several mutable reference types, each having well-defined
semantics for the transition between states.

Clojure was initially conceived as targeting both the JVM and the
CLR. For various reason currently the core development team is targeting mainly
the JVM and the [CLR port](https://github.com/richhickey/clojure-clr)
is receiving less attention (though it's not abandoned and it's
regularly being updated).

# A brief history of Clojure

Clojure is very very young project (compared to most popular
programming languages). It was created in 2007 by Rich
Hickey (project leader and benevolent dictator for life). He developed
Clojure because he wanted a modern Lisp for functional programming,
symbiotic with the established Java platform, and designed for
concurrency. What started as a hobby project turned into some much
bigger with Rich getting some excited about the project that left his
job to work full-time on the project, effectively burning his life's
savings in the process. This was quite the gamble, but it turned out
to be a lucky gamble since Clojure's popularity rapidly spiked and
loyal and energetic community quickly formed around the project. 

Clojure became the new language of choice for many well respected
hackers from different communities. I've noticed something of a trend
in that department - most Clojure hackers used to be Ruby hackers. I
guess some of the Ruby hackers were not satisfied by partial subset of
Lisp features, available in Ruby, and wanted to gain access to all of
Lisp's power.

The current Clojure version is 1.2 with 1.3 being just around the
corner.

# Installing Clojure

Installing Clojure is just a matter of downloading and extracting a
single archive -
[clojure.zip](http://github.com/downloads/clojure/clojure/clojure-1.2.0.zip). Many
high quality Clojure libraries come prepackaged in another archived
named
[Clojure Contrib](http://github.com/downloads/clojure/clojure-contrib/clojure-contrib-1.2.0.zip). Clojure
Contrib is kind of a staging area for Clojure development - it's a
common practice to move some of the best parts of contrib into core.

In the directory in which you expanded clojure.zip, run:

{% highlight console %}
$ java -cp clojure.jar clojure.main
{% endhighlight %}

This will bring up a simple read-eval-print loop (REPL) a.k.a. an
interactive console. Much of
Clojure is defined in Clojure itself (in the **core.clj** file included in
the src directory of distribution), which is automatically loaded from
the .jar file when Clojure starts. The file **user.clj**, if found in the
classpath, will be auto-loaded as well. You can leverage this to cause
code to run when Clojure starts.

When core.clj is loaded you will have the language as described herein fully available.
Try:

{% highlight clojure %}
user=> (+ 1 2 3)
6
user=> (println "Hello, Clojure!")
Hello, Clojure!
nil
user=> (. javax.swing.JOptionPane (showMessageDialog nil "Hello
World"))
{% endhighlight %}

The REPL has very rudimentary editing. For a better experience, try running it via the [JLine](http://jline.sourceforge.net/) ConsoleRunner:

{% highlight console %}
java -cp jline-0_9_5.jar:clojure.jar jline.ConsoleRunner clojure.main
{% endhighlight %}

This will give you left/right arrow key navigation and up/down arrow
command history.

Later on we'll see how to setup a real Clojure development environment
in which you'll be able to leverage the full power of the Clojure REPL
and interactive programming.

# Did you say Clojure was a Lisp???

Most developers tend to have a very negative attitude towards the word
Lisp in general. I guess it spawns all kinds of nasty associations in
their brains - like prefix syntax notation, tons of parentheses and a
lot of crap their heard about Lisp from their 70 year-old professor
teaching introduction to functional programming in college, whose
notion of functional programming is that in Lisp everything is a
function (believe me when I tell you this - such professors do exist).

You know, I wasn't born coding in Lisp myself. When I was initially
exposed to Lisp when I tried to learn the Emacs text editor I was
baffled by many things - the strange syntax, the talk about atoms and
lists, code as data, macros, continuation, tail-call optimizations,
what to quote and that to evaluate. To put it shortly - I was like
Alice down the rabbit whole or like Neo when he found out what the
Matrix is...

The interesting thing is that I felt similarly when I learnt my first
programming language Pascal in the 8th grade. It's not that Lisp is
any harder than the other programming languages - it's just that it's
different and you're usually approaching it from a position in which
you know one or several programming languages using the much more
widespread Algol syntax. I advise to simply keep an open mind while
you read this article and don't just dismiss Clojure because of its
Lisp heritage.

You've likely know at least one person who constantly keeps telling
you how Lisp is the one true programming language, how nothing
compares to it and how Lisp is the actual answer to that fundamental
question about the life, the universe and everything else (not
42). These people might very well be telling the truth, but their
zealous rants tend to create a negative attitude towards the Lisp
community as well. Please, ignore them. 

# Clojure at a glance

_Mutable state is the new spaghetti code!_ - Rich Hickey, creator of Clojure

_Time is the new memory!_ - Rich Hickey

_Clojure feels like a general-purpose language beamed back from the
near future. Its support for functional programming and software
transactional memory is well beyond current practice and is well
suited for multicore hardware. At the same time, Clojure is well
grounded in the past and the present. It brings together Lisp and the
Java Virtual Machine. Lisp brings wisdom spanning most of the history
of programming, and Java brings the robustness, extensive libraries,
and tooling of the dominant platform available today._ - Stuart
Halloway, author of ["Programming Clojure"](http://www.pragprog.com/titles/shcloj/programming-clojure)

* Dynamic language for the JVM
    * Clojure uses dynamic typing like languages such Ruby and Python
      and a very smart compiler that will generally generate very
      efficient bytecode. If you want to push the envelope even
      further you can add some explicit type hints in your Clojure
      code to ensure the generation of even faster bytecode.
* Lisp reloaded
    * Clojure is Lisp down to its core - it has all the features that
      are known and loved and in the same it improves upon them in
      several ways - for instance we have a literal syntax for most
      common collection types. Sure - with Common Lisp's reader macros
      one can do this as well, but nobody bothers to...
* Elegant
    * Clojure code tends to be very concise, but very readable non the
      less. A core idea in Clojure is to strip the incidental
      complexity of problems solving and to be able to just solve the
      problems straight away without much ceremony.
* Functional
    * Clojure puts heavy emphasis on functional programming, but it's
      a practical functional programming language - not a pure one
      like Haskell. Clojure acknowledges that some stuff simply change
      and operations have to generally produce some effects and make
      those thing easy to model. Clojure has a library full of
      rock-solid immutable data structures, relies heavily on lazy
      evaluation and higher-order functions.
* Designed with concurrency in mind
    * Clojure has extensive built-in high-level facilities to deal
      with concurrent access to data and parallel programming in general.
* Fast
* Capable of easily leveraging existing Java code
    * Using Java code from Clojure is direct, easy and
      idiomatic. There are no intermediate layers or the need to
      write wrapper for everything.
      
I'll discuss in greater detail some of those features as I moving along.

# A whirlwind tour of Clojure

**Clojure is elengant**

* Removes a lot of accidental complexity
* Clojure programs are generally expressive and concise
* Concise programs are naturally easier to understand and maintain

Consider this Java example from our Scala discussion:

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

As a reader pointed out using the third party Guava library the code
can be reduced to:

{% highlight java %}
public boolean hasUpperCase(String word) {
    if (null != word)
        return any(charactersOf(word), new Predicate() {
                public boolean apply(Character c) {
                    return isUpperCase(c);
                }
            })
        else
            return false;
}
{% endhighlight %}

It still looks quite ugly to me. For the sake of comparison here's the
Clojure version:

{% highlight clojure %}
(defn has-uppercase? [string]
  (some #(Character/isUpperCase %) string))
{% endhighlight %}

The definition of the problems is "A string has an uppercase character if
some of the characters in it is uppercase" (doesn't sound good, but
will do). The Clojure code reads more or less like the definition of
the problem. A finer point is that it will work correctly even if you
pass **nil** to the has-uppercase? function.

**Clojure is concise**

We already saw in the previous example the conciseness of Clojure
code, but here we'll add another example. This is Java:

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

In Clojure you'd probably model this class like this:

{% highlight clojure %}
user> (defrecord person [name age])
user.person
user> (person. "Bozhidar" 26)
#:user.person{:name "Bozhidar", :age 26}
user> (def me (person. "Bozhidar" 26))
#'user/me
user> (:name me)
"Bozhidar"
user> (:age me)
26
{% endhighlight %}

Clojure's version of the type is a one liner and remain shorter even
with a few examples of its usage. It's not equivalent to Java
definition, however - the Clojure version of the structure is
immutable.

# Clojure is a Lisp

For better or for worse Clojure is a Lisp dialect and we should accept
this. I have always viewed Lisp as weapon from a more elegant era when
people were more concerned with elements of style and empowering the
developers to easily translate their thought into programs. For one
reason or another every Lisp dialect has failed to capture the
attention of a critical mass of developers that may propel it into the
mainstream. This, of course, doesn't mean that existing Lisp dialects
should be considered a failure. Scheme (the dialect that has probably
had the greatest impact on Clojure's design) was designed to be as
simple as possible so it could be appropriate as a teaching tool - in
that area Scheme certainly excelled. Common Lisp was created to bring
together the various Lisp dialects under a common denominator and it
also excelled in that endeavour. I guess that its creators hoped that
it would capture a significant market share at some point, but alas -
that never happened. 

The syntax and programming model of Lisp so far have been too much for a
typical developer to absorb. Yet, there’s something special about
Lisp that’s worth revisiting, so the new dialects continue to
emerge. Some of the best programming universities lead with the Lisp
language to form young minds while they are still open. I have
witnessed something of a cycle - every 5 or so years the interest in
Lisp spikes because of something. In the beginning of the nineties the
work on Common Lisp excited a lot of developers. Five years later Paul
Graham took the stage - he showed the world how Lisp can empower small
teams and make real money. Five years ago Peter Seibel published the
"Practical Common Lisp" book that appeared on Amazon's bestseller list
and got a lot of new developers excited about Lisp. A now... well I
guess you can figure that out on your own. 

Lisp just won't let go and die. There is something magical about
it. And there is this inexplicable smugness on the face of Lisp
developers...

So let's review the typical Lisp features that are present in Clojure:

* Lisp-1 dialect
    * This means that functions and variables share the same
      namespace, unlike in dialects like Common Lisp. Both approaches
      have their merits and drawbacks as usual. In Clojure you cannot
      have a variable named the say way as a function, but you can
      pass function names around without any special syntax. In Common
      Lisp you can have function and variables sharing the same name,
      but you have to mark functions explicitly when you're passing
      them around.
* Dynamic - both in term of dynamic typing and dynamic
  development. Lisp is the language that made popular the technique of
  incremental interactive development (we'll talk about it more in a bit)
* Code is data
    * List code is defined in term of Lisp data structures. When the
      reader read the source code of the application it converts it to
      standard Lisp objects and they represent the program. No special
      transformations, no AST. This is the heart of Lisp macros and a
      centerpiece in Lisp philosophy.
* Reader
    * The reader can read valid Clojure forms and translate them into
      Clojure objects - object, function call, everything that has a
      readable representation
* Small core, next to none syntax
    * In terms of compact syntax and uniformity of the syntax it has
      always been hard to beat Lisp
* Sequences
    * Clojure abstracts common collection traits into an abstraction
      called seq which allows you to use a similar API for many tasks
* Macros
    * Forget about C marcos, Word macros, editor macros. Lisp macros
      are the most powerful metaprogramming technique out there - they
      enable you generate new syntax abstractions unlike anything else
* Syntactic abstractions

# Persistent data structures

Data structures in Clojure are immutable. Operations executed on them
return a new data structure of the same type instead of modifying the
structure in place. Understandably most people are immediately
concerned about the performance implications of such a technique -
this seems like quite a lot of overhead. They needn't worry, though.

Data structures in Clojure are persistent. A persistent data
structure is a data structure which always preserves the previous
version of itself when it is modified; such data structures are
effectively immutable, as their operations do not (visibly) update the
structure in-place, but instead always yield a new updated
structure. A persistent data structure is not a data structure
committed to persistent storage, such as a disk; this is a different
and unrelated sense of the word "persistent.".

Persistent data structures save a lot of copying around and improve
greatly the performance. 

The core data structures are:

* List
* Set
* Map
* Vector

Let's see them in action:

# Functional programing with Clojure

# Parallel programming

# Interactive development

* REPL
* Functions can be defined in real time
* Loading & compilation of code at runtime
* Powerful introspection features
* Interactive development

# The tools of the trade

The single biggest problem with Clojure in the moment (at least in my
opinion) has nothing to do with the language itself. The problem is
the lack of decent tooling and infrastructure around it. Lisp hackers
have traditionally favoured the SLIME development environment for
Emacs. Unfortunately the maintainers are not especially interested in
having Clojure support(since SLIME targets Common Lisp) and nobody in
Clojure community seems to be capable of writing an adequate swank
component for Clojure. The existing one is quite rudimentary and
doesn't work with stock SLIME distributions. But this is not the worst
part - the worst part is that even this crippled SLIME is still the
best development tool for Clojure. IntelliJ's plug-in is almost
unusable, Eclipse's is barely usable and NetBeans's cannot be
installed half the time...

* IDEs
   * IntelliJ IDEA
   * Eclipse
   * NetBeans
   * SLIME

Luckily there's no lack of good build tools that one can use with Clojure.

* Build tools
   * Apache Maven
   * Leiningen
   * Cake
   * Gradle
   * Apache Builder
   
# Epilogue
