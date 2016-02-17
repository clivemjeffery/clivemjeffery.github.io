---
layout: post
title: Ruby on Rails
---

## Setup On El Capitan

This is my setup experience on a new install of OS X El Capitan. Well, not quite new, I'm using a MacBook Pro which had the El Capitan Beta. Now I've installed the production El Capitan over the top and "About This Mac" reports OS X 10.11.3.

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

### Various

Looks like this might be a good sequence: https://www.reddit.com/r/ruby/comments/3n26gt/upgrade_to_el_capitan_with_homebrew_ruby/

### RVM

Reading the [RVM install guide](https://rvm.io/rvm/install), some do-it-all rails installers are mentioned but the [RailsInstaller](http://railsinstaller.org/en) one comes with warnings about OS X Mavericks and does not list El Capitan in the Mac Downloads section. I think I'll go with RVM and install rails from there.