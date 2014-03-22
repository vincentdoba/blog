---
layout: post
title:  "Install latest version of Ruby using RVM with ansible on Debian 7"
date:   2014-03-22 11:00:00
categories: ansible ruby
---

This post will describe the role used to install the lastest stable version of ruby, currently 2.1.1 version.

First, the directory tree : 

ruby/tasks/main.yml

As you can see, there is only one file, main.yml. Here is the complete main.yml file :

{% highlight yaml %}
---
- name: Install system ruby version
  apt: pkg={{ item }} state=present
  with_items:
    - curl
    - ruby

- name: Install latest stable ruby version
  shell: "\\curl -sSL https://get.rvm.io | bash -s stable --ruby"

- name: Remove system ruby version
  apt: pkg={{ item }} state=absent purge=yes
  with_items:
    - ruby
    - ruby1.9.1
    - libruby1.9.1
{% endhighlight %}

Let's detail this file.

First, to install latest ruby, RVM needs ruby and curl installed. We will just install the debian version of ruby, which is the 1.9.1 on debian Wheezy, and curl via the apt module. So we add the following task :

{% highlight yaml %}
- name: Install system ruby version
  apt: pkg={{ item }} state=present
  with_items:
    - ruby
    - curl
{% endhighlight %}

Note that we used with_items in order to install several packages at once. After this task, we will install rvm using the command available in the [official rvm website][http://rvm.org]. 

{% highlight yaml %}
- name: Install latest stable ruby version
  shell: "\\curl -sSL https://get.rvm.io | bash -s stable --ruby"
{% endhighlight %}

And finally, we remove the no more needed ruby package from system

{% highlight yaml %}
- name: Remove system ruby version
  apt: pkg={{ item }} state=absent purge=yes
  with_items:
    - ruby
    - ruby1.9.1
    - libruby1.9.1
{% endhighlight %}

That's all, now at your next login to the machine you will have the latest stable version of ruby in your path

Note :

To use latest ruby version in your future shell task in ansible, don't forget to add a dependance to the ruby role, and to modify path in order to take directory /usr/local/rvm/rubies/default/bin and /usr/local/rvm/bin, as the following example :

{% highlight yaml %}
- name: Install bundler
  shell: "gem install bundler"
  environment: 
    PATH: "/usr/local/rvm/rubies/default/bin:/usr/local/rvm/bin:/usr/bin:/bin:/sbin:/usr/sbin:/usr/local/bin:/usr/local/sbin"
{% endhighlight %}
