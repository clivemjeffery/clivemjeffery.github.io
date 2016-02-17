---
layout: post
title: Ruby on Rails
---

## Setup On El Capitan

This is my setup experience on a new install of OS X El Capitan. Well, not quite new, I'm using a MacBook Pro which had the El Capitan Beta. Now I've installed the production El Capitan over the top and "About This Mac" reports OS X 10.11.3.

There are likely to be some do-it-all rails installers like [RailsInstaller](http://railsinstaller.org/en). It has warnings about OS X Mavericks and does not list El Capitan in the Mac Downloads section. I think I'll go with a piecemeal approach.

From what I know already and [Galtzo's upgrade guide](https://www.reddit.com/r/ruby/comments/3n26gt/upgrade_to_el_capitan_with_homebrew_ruby/), here's the sequence.

### Developer Tools

Apple Developer Tools are always needed for various RoR and other homebrewing activities. So I'll get those first. This [OSXDaily guide](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/) seems to offer a simple way to get them.

~~~
$ xcode-select --install
~~~

After that, I verified just one of the installed binaries, git. It was found by a `which git` beforehand but raised a path error on attempted `git --version`. Now the following was reported.

~~~
$ git --version
git version 2.5.4 (Apple Git-61)
~~~

### Java - get a  JDK

A JDK might come in handy, especially if I want to run a JRuby. Shoes 4 uses JRuby so I'll get this now. RubyMine is a Java app too. So I did the `java` thing in terminal, opened the web page, downloaded and installed the latest JDK (8 74). The installer passed on a link to some developer's [getting started](http://docs.oracle.com/javase/tutorial/getStarted/index.html) resources; they might be useful later.

### Homebrew

OK, now for [Homebrew](http://brew.sh). My `/usr/local` is empty so it will be easy to see brew packages arriving. I already have a ruby (2.0.0p645) but I'm not sure if I installed it in the Beta or not. Now, from the homepage, I'll try:

~~~
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
~~~

This reported `installation successful`. I followed with the Qt5 install recommended by Galtzo for Capybara. It all seemed to work and `qmake` is available.

### GPG

RVM now requires `gpg` and it looks like homebrew can install it. Here goes:

~~~
$ brew install gpg
~~~

This got me GnuPG 1.4.20

### RVM

First, install Michal Papis' key.

~~~
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
~~~

Then RVM. Shall I get rails with it?

~~~
$ \curl -sSL https://get.rvm.io | bash -s stable --rails
~~~

Most of this seemed to work. The script stalled up on and took ages for the final part, installing the ri documentation for rails. Nevertheless, it did finish and I now have a local ruby managed by rvm.

~~~
$ rvm list rubies
rvm rubies
=* ruby-2.2.1 [ x86_64 ]
# => - current
# =* - current && default
#  * - default
~~~

I also have rails 4.2.5.1. Time to test it!

### Postgres

First, of course, I'll need Postgres. Galtzo recommended the [Postgres App](http://postgresapp.com), although it could be installed with Homebrew. I'll go with the app. Downloaded, moved to Applications, run and set the auto-start option.