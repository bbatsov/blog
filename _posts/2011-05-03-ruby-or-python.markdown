---
layout: post
title: "Ruby or Python? Well, it depends..."
---

**Disclaimer**

_If you're looking for a flame post - this is not one of them. I love
both languages and I'll simply compare some of their features and
possible uses._

Ruby or Python? This is the Question! Well it might not be the
Question, but it's a common question for many developers looking to
break free from the statically typed language they know and learn a
dynamic language. I personally know them both(though I know a bit more
Ruby, than Python) and in this article I'll share my personal opinion
on their strengths and weaknesses. You'd probably do good to learn
them both, but my arguments here may lead you to pick only one of the
languages depending on you preferences.

#Syntax & code structure

Ruby makes heavy use of braces and keywords(like do/then/end) to
delimit blocks of code. Python relies simply on indentation. 

{% highlight python %}
def fact(n):
    return reduce(lambda x, y: x * y, range(1, n + 1))
{% endhighlight %}

Same thing in Ruby:

{% highlight ruby %}
def fact(n)
  (1..n).reduce(:*)
end
{% endhighlight %}

I personally prefer the Python approach since it enforces the code
semantics based on the code structure alone without imposing special
syntax.

As a side node you might take under consideration that the Ruby method
definition doesn't have an explicit return value. The value of the
last expression in the method's body becomes automatically the
method's return value. Lisp developers will find this familiar. Java
and C# developers will probably find it a bit confusing. There is a
_return_ in Ruby, though, it's just rarely used.

Both languages have support for nested function definitions. 

Both languages have support for "top-level" functions - that live(or
seem to live) outside classes and modules(something not possible in
Java for instance). This makes them good for general purpose
scripting. While I would still prefer to do my system administration
with shell and Perl scripts - Ruby and Python offer a solid
alternative. Python has a richer system administration library so I'd
prefer it over Ruby for such tasks. 

Ruby has a lot of crust("heritage") from Perl - like a myriad of special
variables that are now more or less deprecated. It also has much syntactic
sugar. For instance predicate methods(those that return true or false)
have name that end with ?(usually) like even?, odd?, prime?,
etc. Methods that mutate the object on which they were invoked
generally have the ! suffix - sort!, map!, etc. I find this a nice
decision. In Ruby you generally have many ways to achieve the same
result:

{% highlight irb %}
ruby-1.9.2-p0 > 1.even?
 => false 
ruby-1.9.2-p0 > arr = [1, 2, 3]
 => [1, 2, 3] 
ruby-1.9.2-p0 > arr.map { |x| x * 2 }
 => [2, 4, 6] 
ruby-1.9.2-p0 > arr
 => [1, 2, 3] 
ruby-1.9.2-p0 > arr.map! { |x| x * 2 }
 => [2, 4, 6] 
ruby-1.9.2-p0 > arr
 => [2, 4, 6] 
ruby-1.9.2-p0 > (1..5).reduce(:*)
 => 120 
ruby-1.9.2-p0 > (1..5).reduce { |x, y| x * y }
 => 120 
ruby-1.9.2-p0 > (1..5).reduce do |x, y|
ruby-1.9.2-p0 >     x * y
ruby-1.9.2-p0 ?>  end
 => 120 
{% endhighlight %}

No such things in Python, however. Python's philosophy is one of
simplicity - no excessive syntax sugar, one true way of doing things.

Both languages have powerful features for organising code in
libraries. I would not go into any details on the subject here, but
I'll share with you the fact that I like Python's more.

Both languages come with a REPL in which you can do some exploratory
programming. Ruby's REPL(irb)  allows you
to do TAB smart completion(amongst other things) by default. To get
TAB completion in the Python REPL you'd have to execute this bit of
code first:

{% highlight pycon %}
>>> import readline, rlcompleter
>>> readline.parse_and_bind("tab: complete")
{% endhighlight %}

Alternative you can just stick this code snippet in the
**~/.pythonrc.py** file(create it if it doesn't exist). If you are using
Windows adjust accordingly(you will have to figure out where
pythonrc.py is located there).

Ruby does not have statements - only expressions. This
basically means that everything(objects, method calls) evaluate to
some value(though the value might not be helpful always). 

In Python there are some statements such as assignment and _if_. One
thing I dislike about the Python REPL is that it doesn't print None
values. Compare this bit of Python code:

{% highlight pycon %}
>>> print("this is a test")
this is a test
{% endhighlight %}

to this Ruby snippet:

{% highlight irb %}
ruby-1.9.2-p0 > puts "this is a test"
this is a test
 => nil 
{% endhighlight %}

In the Python version we see only the side-effect(the printing), but
not the return value.

Python also ships with a minimalistic IDE called IDLE. If you don't
have it by default after a python installation on Linux probably
you're vendor decided to package IDLE as a separate package. IDLE
offers basic features like syntax highlighting, code completion and
integration with a debugger. It's a good tool for exploratory
programming, but I advise you to pick another tool for serious development.

#Naming conventions
The naming conventions for both Ruby and Python are mostly the same
which is good if you're using them both on a daily basis - less room
for confusion.

* variable and method names consisting of more then one word are
  written in lowercase with underscores separating the individual
  words like_this.
* Class names start with capital letter and follow the camel case
  naming convention LikeThis. Some of Python's core classes, however,
  violate this convention.
* Constants are generally written in all caps with underscores
  separating the individual words LIKE_THIS.
  
As I mentioned earlier it's customary to add ? as a suffix to
predicate methods and ! to mutator methods in Ruby. This convention is
not always followed unfortunately, even in Ruby's standard library.

#OOP support
Both Ruby and Python are famous members of the family of object
oriented languages. Unlike languages such as Java and C#, however,
Ruby and Python are pure OOP languages. There is no distinction
between primitive types(such as numbers, characters and booleans) and
reference types(classes). Everything in them is an object and in that
sense it's an instance of some class:

{% highlight pycon %}
>>> type(1)
<type 'int'>
>>> type("string")
<type 'str'>
>>> type(20.07)
<type 'float'>
>>> type([1, 2, 3])
<type 'list'>
>>> type((1, 2, 3))
<type 'tuple'>
{% endhighlight %}

And in Ruby:

{% highlight irb %}
ruby-1.9.2-p0 > 10.class
 => Fixnum 
ruby-1.9.2-p0 > "string".class
 => String 
ruby-1.9.2-p0 > [].class
 => Array 
{% endhighlight %}

As you can see core Ruby classes tend to have a bit more standard and
descriptive names than their Python counterparts. You can also notice
that in Python for some task we use built-in functions like type,
instead of method calls. The built-in function will eventually result
in a method invocation(like "string".__class__ in the case of
type("string")), but I find this irregularity in the syntax a bit
irritating.

Method invocation is more flexible in Ruby - you can omit braces in
some scenarios. This is handy when you're designing a DSL or you're
trying to implement the uniform access patterns(data should be
accessed through fields and methods in the same manner(read this as
with no braces in method invocations)). On the other hand Python's
uniform syntax makes it easier to spot method invocations. 

Both languages don't have operators - just methods. Ruby's OO support
seems to be a bit more mature and polished(at least to me), but
Python's has some touches as well. I particularly like the explicit
self references that are required when you try to access class
members. I'm not too found of the use of special sigils in Ruby to
mark instance(@) and class members(@@). Though they make them visually
distinctive I think we could have lived without them - I'm generally
not a fan of non-uniform syntax rules(and you guessed it - my
favourite language is Lisp).

Ruby's metaprogramming model arguably gives it an edge in the OOP
department, but I won't be discussing the metaprogramming issues here
since they are quite lengthy.

# Functional programming support

Functional programming has been on the rise lately and it's useful to
examine what kind of support both languages provide for it. Both have
support for lambda functions and respectively - higher-order
functions(functions that accept functions as parameters). Ruby has
code blocks, Python has list comprehensions(generally favoured over
higher-order functions). Both languages lack in their standard libs
the immutable data structures that generally are the code of most
functional programming languages. Here's a few example related to
filtering a sequence based on some predicate:

{% highlight pycon %}
>>> filter(lambda x: x % 2 == 0, range(1, 11))
[2, 4, 6, 8, 10]
>>> [x for x in range(1, 11) if x % 2 == 0]
[2, 4, 6, 8, 10]
{% endhighlight %}

Ruby:

{% highlight irb %}
ruby-1.9.2-p0 > (1..10).select { |x| x.even? }
 => [2, 4, 6, 8, 10] 
ruby-1.9.2-p0 > (1..10).select &:even?
 => [2, 4, 6, 8, 10] 
{% endhighlight %}

Ruby's functional programming support seems to be better to me, but
this is of course subjective.

# GUI programming

Python has tkinker by default - a wrapper around the Tk library(which
sucks in my humble opinion). Ruby doesn't have even this much. Both
have binding for the popular GUI toolkits such wxwidgets, GTK,
QT. From my experimentation with them I can tell you that you'll be
much better off with Python in that department. It's not wonder that
many GTK+ applications these days are implemented in Python. Most Ruby
bindings projects seem to be in a state of disarray, abandonment - I
guess we have to thank Rails for that. Most people think of Rails as
the only use of Ruby which is sad...

Ruby devs shouldn't despair however. JRuby(Ruby's port to the JVM) has
an excellent support for the superb Swing GUI framework and MacRuby
has great support for building Cocoa Apps for OS X. I personally think
that JRuby is the best Ruby distribution out there, but that's the
point of another post entirely.

# Misc

In terms of performance of the default interpreters CPython and MRI
Ruby Python is the clear winner. One should note, however, is that there
are many how quality implementation of Ruby and Python for different
platforms where the performance situation differs wildly. For instance
Jython is much slower that JRuby. With the addition of invoke_dynamic
in JDK7(basically bytecode level support for dynamic method dispatch)
the performance of JRuby and Jython could potentially be improved
greatly.

In terms of overall usage, market share, job offers and sheer size of
the community and available libraries Python is ahead of Ruby as
well. One of the main supporters of Python is after all none other
than the mighty Google. Ruby has also the unfortunate luck to be
living in the shadow of a single application written in Ruby - Ruby on
Rails, that is arguably more popular than the language itself.

Tooling for dynamic languages is currently not as advance as the one
for static languages. People often joke that Python(Ruby) > Java(C#),
but Python + any python IDE < Java + IntelliJ
IDEA(Eclipse/NetBeans). Python and Ruby IDEs seem to be mostly on par
currently. I do all of my Ruby and Python coding in Emacs, but I do
like RubyMine and PyCharm. 

Since they are often used for the creation of webapps one should
consider the deployment issue. Most web hosting companies provide
cheap Python hosting, but very few companies provide Ruby hosting.

# The Python 3 problem

Python 3 was a great undertaking that improved on a lot of aspects of
the language(for example Unicode support) and the standard library. To
do this it dropped backward compatibility, an act that slowed it's
adoption immensely. Three years have passed since it's release and
still most hosting providers, Linux distros and Python projects hold
on to the older 2.7.x Python branch.

This is a bit of tragedy since Python 3 is truly a great improvement
over Python 2. I mention this because most recent books are written
with Python 3 in mind, but if you land a Python jobs somewhere chances
are you'll have to use Python 2.x.x for the foreseeable future.

# Conclusion

Ruby and Python are two beautifully engineered languages capable of
just about everything. If you don't know any of them you'll do well to
learn at least one. If you know only one it might not be a terrible
idea to learn the other.

I haven't touched on many language features(like Python generators and
Ruby mixins), but to be honest I'm just tired of typing. One good
place to start your journey to Python is
["Dive into Python 3"](http://diveintopython3.org/). For Ruby
beginners I'd recommend a copy of ["The Ruby Programming Language"](http://www.amazon.com/Ruby-Programming-Language-David-Flanagan/dp/0596516177).
