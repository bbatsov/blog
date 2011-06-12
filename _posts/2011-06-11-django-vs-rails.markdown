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
position in the company is Technical Lead - the people responsible for
the selection of technologies around which the projects are being
build. Since we'll be doing mostly web development we've had a long
discussion with the companies CTO about the direction which we should
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

Hopefully this article will be useful to people that are in the same
boat as was - picking between Rails and Django.

## Setup & Getting started

# Rails

**Linux & OSX**

The recommended way to install Ruby on Rails 3.x is via [RVM]().

rvm get 1.9.2
rvm use 1.9.2
gem install rails
rails -v

rails new railsdemo

# Django

**Linux**

yum install Django

**Windows**

Bitnami windows stack.

django-admin startproject djangodemo

## Features at a glance

## Community

## Tooling

Traditionally Ruby & Python hackers have been hacking with just a
powerful programmer's editor like Emacs, vim or TextMate. While there
is nothing inherently wrong with this approach (I'm an avid Emacs user
myself), I do find IDEs quite helpful when working on larger code
bases with their trademark features such as intelligent
autocompletion, safe refactorings, on-the-fly syntax checking, etc. So
here's what we've got:

- [RubyMine]() - hands down the best Ruby and Rails IDE I've ever
  used. The [list of features]() is epic as is the quality of the
  project. It support Rails 3, git, RSpec, Cucumber, sass, haml and
  many other cool Ruby/Rails related technologies. Sure, it's a
  commercial project, but is priced very reasonably. 
- [Aptana Studio]()
- [Komodo]()
- [PyCharm]() - from the same company that develops RubyMine, PyCharm
  is the king of IDEs when it comes down to Python. It has full
  featured Django support - there is even autocompletion in the Django
  templates.
  
  

## Epilogue
