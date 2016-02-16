---
layout: post
---
### Intialising a new image

Most of this stuff is from <https://www.raspberrypi.org/documentation>
Check it out if things go wrong or you've forgotten a step.

Find the disk number of the sd card with

~~~
mac$ diskutils list
~~~

and install to sd card with

~~~
mac$ sudo dd bs=1m if=2015-05-05-raspbian-wheezy.img of=/dev/rdiskN
~~~

from my `Disk\ Images` folder where `N` is the disk number for the sd card.

Log into the pi via ssh and run raspi-config to expand the file system,
set the hostname and so on.

[Fing](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=en) on my phone finds the new pi better than the bthomehub finds it in Home Network (must find out why, at some point).

Check how much disk is used (and remember ready for the upgrade step next).

~~~
pi$ df -h
~~~

Update and upgrade the install with

~~~
pi$ sudo apt-get update
pi$ sudo apt-get upgrade
~~~

The pi docs warn that there might not be enough space for the upgrade, though I've not encountered this yet. You need check the space required is available and either continue or abort when prompted by the step above. If there isn't enough space, then

~~~
$ sudo apt-get clean
~~~

will remove any old package archives and might free up enough. Probably a good idea to reboot after this.

### Useful Tools

#### VNC

Install tightvncserver and my runner script with

~~~
pi$ sudo apt-get install tightvncserver
~~~

~~~
mac$ scp vncs.sh pi@piname:/home/pi
~~~

on the mac in the same folder as this text file. The content of the `vncs.sh` shell script is quite minimal and just launches sthe server with some settings I find work for me.

~~~
#!/bin/sh
vncserver :0 -geometry 1920x1080 -depth 24
~~~

#### Configure Git

~~~
pi$ git config --global user.name "clivemjeffery"
pi$ git config --global user.email "clive@rosedene.com"
~~~

which set my github credentials, and

~~~
pi$ git config --global credential.helper cache
~~~

which will cache passwords for 1 hour (extended from default of 15 mins). These require git version 1.7.10 and the latest wheezy has 1.7.10.4 so it should work. It might also be good to set the line-ending behaviour with

~~~
pi$ git config --global core.autocrlf input
~~~

The same thing can be done on Windows with true as the argument. Even better might be a per-repository setting in a .gitattributes file, see [here](https://help.github.com/articles/dealing-with-line-endings).

After this I can get a github project like qbike with

~~~
pi$ git clone https://github.com/clivemjeffery/qbike.git
~~~

#### Python Utilities

The python utilities [pip](https://pip.pypa.io/en/stable/) and [setuptools](https://pypi.python.org/pypi/setuptools) are essential for qbike and will be pretty useful for any python development.

~~~
$ sudo apt-get install -y python-setuptools
$ sudo apt-get install python-pip
~~~

It seems that `pip` is more modern than `setuptools` but it is best to have both. 