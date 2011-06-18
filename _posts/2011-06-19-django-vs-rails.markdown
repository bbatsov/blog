---
layout: post
title: "Django 1.3 vs Rails 3: A not so final showdown"
categories:
- Ruby
- Rails
- Python
- Django
---

## Overture

I've recently started a new job at an American start-up company. My
position in the company is Technical Lead - the person responsible for
the selection of technologies around which the projects are being
built. Since we'll be doing mostly web development we've had a long
kick-off discussion with the company's CTO about the direction which we should
initially take. He had PHP in mind, but I convinced him that Ruby or
Python would make much better platforms for our futures apps. So he
tasked me to research the two leading frameworks in the Ruby and
Python land - namely Ruby on Rails 3 and Django 1.3. I had a week to
prepare some prototypes with both and create on overview for my
boss. I had some experience with Rails 2 a few years back and I have
fairly decent knowledge of Ruby. My Python is not as fluent
(admittedly), but still - I've played a lot with Python
recently. Django, however, was completely new to me. In this article
I'll try to compare the frameworks in a totally friendly way. If I've
written something that is wrong - please feel free to correct me.

Please, keep in mind that a short comparison article cannot even begin
to scratch the immense complexity of such frameworks. The overview,
that you'll find here is a bit on the superficial side, but it should
give you enough pointers to get you started.

Hopefully this article will be useful to people that are in the same
boat as was - picking between Rails and Django.

## Setup & Getting started

# Rails

**Linux & OSX**

The recommended way to install Ruby on Rails 3.x is via
[RVM](https://rvm.beginrescueend.com/). RVM allows you to have several
version of Ruby installed at the same time and to easily switch
between them. It also allows you to create gem sets, which are quite
handy in testing. After you've installed RVM it's easy to install any
Ruby interpreter and Rails. This example shows how to get MRI 1.9.2
and Rails:

{% highlight console %}
$ rvm get 1.9.2
$ rvm use 1.9.2
$ gem install rails
$ rails -v
{% endhighlight %}

Open your browser and type localhost:3000 as the url.

At this point you should probably either start playing with
scaffolding or read the rest of this article and start playing with
scaffolding afterwards :-)

**Windows**

While there are many ways to get Ruby on Rails installed on a Windows
host the simplest is certainly the [RailsInstaller](http://railsinstaller.org/). It has only one
little drawback - currently it comes with Ruby 1.8.7 bundled, but the
current beta already features Ruby 1.9.2. 

**Your first Rails app**

{% highlight console %}
$ rails new railsdemo
$ rails s
{% endhighlight %}

# Django

**Linux**

I prefer to install django from the distribution's package manager. On
a Red Hat distro like Fedora I would do:

{% highlight console %}
$ sudo yum install Django
{% endhighlight %}

And on a Debian system:

{% highlight console %}
$ sudo apt-get install python-django
{% endhighlight %}

A popular alternative is to this distro-specific approach is to use a
python package manager like [easy_install](http://packages.python.org/distribute/easy_install.html) or [pip](http://pypi.python.org/pypi/pip).

**Windows**

The [Bitnami Django stack](http://bitnami.org/stack/djangostack) is the simplest way to get Django and
everything that it requires in a single step.

**Your first app**

{% highlight console %}
django-admin startproject djangodemo
{% endhighlight %}

## Features at a glance

# Rails

The centerpiece of Rails's philosophy is called convention over
configuration(CoC). This basically means that a Rails projects has a
predefined layout and sensible defaults. All components (models,
views, controllers, layouts, css, javascript, etc) have standard
places where you drop them and the application picks them up without
any additional effort on your part. 

People seem to underestimate the importance of CoC in practice - it
makes it a lot easier to reason about a project and a lot easier to
configure the project. On the other hand if some of the defaults don't
work for you - you'd have to jump through some hoops. Recent versions
of Rails, however, have made it a lot easier to tweak the defaults.

Rails is a classical Model-View-Controller full stack web
framework. What separates it from most of the MVC frameworks around is
the heavy emphasis on REST. The domain objects are treated as
resources and could be handled in a uniform manner using just the
standard HTTP verbs like GET, PUT, DELETE, POST.

The model layer is the home of your domain objects and the business
logic surrounding them. Domain objects (a.k.a. entities) are mapped to
database tables (at least in RDBMS). Unlike most object relational
mappers Rails's ActiveRecord (the default ORM, could be substituted
with something else if you wish) doesn't require you to explicitly
declare the structure of the objects, but rather extracts it
automatically from you DB table definitions. A simple class, modeling
an application user might look like this:

{% highlight ruby %}
class User < ActiveRecord::Base
  validates :first_name, :last_name, :email, :password, :presence => true
  validates :password, confirmation: true
end
{% endhighlight %} 

Note that the validation methods are entirely optional (but highly
recommended) - the class could have very well had an empty body. Rails
would know to look for a table named Users in the database and extract
the field information from it.

In the view layer Rails has traditionally relied on HTML templates
with Ruby code embedded in them (html.erb). There are a lot of
community contributed alternatives, however, with HAML being the most
prominent one. 

Rails features tight integration with JavaScript and AJAX. Versions
prior to 3.1 shipped by default prototype and scriptaculous. In
version 3.1 jQuery replaced them as the default JavaScript library.

Rails is extendable through a multitude of community supplied plugins
that could add incredible functionality to your apps for free. Some of
my favorite plugins are [jQuery for Rails](https://github.com/indirect/jquery-rails),
[client side validations](https://github.com/bcardarella/client_side_validations) and [Rails Admin](https://github.com/sferik/rails_admin).

What I particularly like about Rails is that it heavily promotes
testing your code. All of the Rails generators would generate test
stubs, that you'll do to fill in. Rails supports all major Ruby test
suites - Test::Unit, RSpec, Cucumber. You have fixtures support, test
database support, the ability to run unit and functional test
separately. I don't recall using any other framework that pays as much
attention to having tests as Rails and for that I can only
congratulate them.

There are two major version of Ruby out there presently - Ruby 1.8.7
and Ruby 1.9.2. Ruby 1.9.2 offers substantial language and performance
improvements, so you should be pleased to hear that Rails supports
both major Ruby versions. Rails 4.0 will drop support for Ruby 1.8.x.

The most common deployment options for Rails are currently Apache
HTTPD or NginX and Phusion Passenger (mod_rails). People shopping for
cloud Rails deployment should definitely take a look at Heroku.

Rails also run on alternative Ruby implementations like JRuby and
Rubinius, that offer exciting new possibilities. For instance using
JRuby allows you to deploy a Rails app into a Java application server
like JBoss or Glassfish and to tap into all those great Java libraries
and frameworks around. Using JRuby also gives you the opportunity to
deploy your apps on Google's App Engine.

# Django

While I had some experience with Rails from a couple of years ago,
Django was something totally new to me. I expected it to be more or
less Rails for Python, but when I created my first Django app I was
surprised to see that the project folder consisted of only three
files.

While Django is a MVC controller framework as well it's built around a
different mindset. Django is totally configurable and minimalistic
framework that empowers the developers to tailor it to their needs. 

A Django project is comprised of autonomous and reusable apps. Apps on
the other hand are comprised of models, views and templates. Django
differs a bit in terminology with Rails - the Rails controllers are
views in Django and the Rails view are called templates in Django. You
can sometimes hear that Django is a Model-View-Template framework -
that shouldn't confuse you. Although the terminology is different the
principles are the same.

Django's ORM is somewhat reminiscent of frameworks like
hibernate. Entity classes declare explicitly the all the attributes.

{% highlight python %}
from django.db import models

class User(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    email = models.EmailField
    password = models.CharField(max_length=30)
{% endhighlight %}

Django has doesn't adhere to the Rails CoC philosophy. It's assumed
that developers know best what layout and configurations options make
the most sense in their applications. I haven't played that much with
Django yet, but I still haven't come by two different Django apps that
are structured in the same manner. While I understand the benefits of
Django's approach I still prefer Rails's approach. I've worked long
enough to know that you're rarely in the position to make better
decisions about the structure and the defaults of your app than the
exceptional developers with huge experience that develop frameworks
like Rails (and Django).

Django has a built-in support to generate an admin UI for your
website. This is a very useful feature indeed and is supported in
Rails as well through plugins (I've mentioned the one I like the best).

Some of you probably know that Python is currently at a bit of a
crossroads. Python 2.x was the stable Python version for many years,
but recently it was replaced by Python 3.x. Python 3.x is all around
great in my personal opinion, but unfortunately it's backward
incompatible with the older 2.x series. For that reason very few high
profile project still don't support it - Django is one such
project. The current version 1.3 require at least Python 2.4 and will
run will every Python up to 2.7. This is a bit of a disappointment
since you'll be missing on a few very cool new features. On a more
positive note Python 2.7 did backport some goodies from Python 3, so
not all is lost. I've read (at totally unofficial places) that Django 2.0 will be targeting Python 3
and I expect it will be available in about a year.

Python is quite mature technology and offers you a nice array of
deployment options - Apache, Nginx and my favorite - Google App
Engine. Python, being one of the two supported languages on the App
Engine (the other one is of course Java) makes it very easy to deploy
Django apps on the App Engine (though you'll need the Django support
for non-relational dbs to be able to use it). 

## Community

When you're selecting the technology for a major project you have to
make sure that the technology is in good shape - there is a solid
community around it, there is no lack of support, innovation and
deployment options.

Both
[Google trends](http://www.google.com/trends?q=ruby+on+rails%2C+django+python)
and stackoverflow.com indicate that Rails currently has larger
community than Django. 

## Tooling

Traditionally Ruby & Python hackers have been hacking with just a
powerful programmer's editor like Emacs, vim or TextMate. While there
is nothing inherently wrong with this approach (I'm an avid Emacs user
myself), I do find IDEs quite helpful when working on larger code
bases with their trademark features such as intelligent
autocompletion, safe refactorings, on-the-fly syntax checking, etc. So
here's what we've got:

- [RubyMine](http://www.jetbrains.com/ruby/) - hands down the best Ruby and Rails IDE I've ever
  used. The [list of features](http://www.jetbrains.com/ruby/features/index.html) is epic as is the quality of the
  project. It support Rails 3, git, RSpec, Cucumber, sass, haml and
  many other cool Ruby/Rails related technologies. Sure, it's a
  commercial project, but is priced very reasonably. 
- [Aptana Studio](http://www.aptana.com/)
- [Komodo](http://www.activestate.com/komodo-ide)
- [PyCharm](http://www.jetbrains.com/pycharm/) - from the same company that develops RubyMine, PyCharm
  is the king of IDEs when it comes down to Python. It has full
  featured Django support - there is even autocompletion in the Django
  templates.
  
## Resources

# Rails

* [Rails Guides](http://guides.rubyonrails.org/)
* [Rails Tutorial](http://ruby.railstutorial.org/)
* [RailsCasts](http://railscasts.com/)

# Django

* [Official Docs](https://docs.djangoproject.com/en/1.3/)

## Epilogue

Chosing Django or Rails is basically a win-win situation - you cannot
go wrong. There are two many similarities between the frameworks and
the differences are not something paramount.

Rails places a heavy emphasis on convention over configuration,
provides you with more defaults and does a can do a lot of heavy
lifting for you automagically. 

Django on the other hand let's you specify most configuration details
yourself, without making the configuration burdensome (like that of
older Java web frameworks).

I guess in the end it really boils down to two things - whether you
like Ruby or Python better and whether you like the defaults imposed
to you by Rails 
