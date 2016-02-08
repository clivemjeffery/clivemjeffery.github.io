---
layout: post
---
# General First Steps On A New Raspbian Image

Most of this stuff is from <https://www.raspberrypi.org/documentation>
Check it out if things go wrong or you've forgotten a step.

Find the disk number of the sd card with

~~~
$ diskutils list
~~~

and install to sd card with

~~~
$ sudo dd bs=1m if=2015-05-05-raspbian-wheezy.img of=/dev/rdiskN
~~~

from my Disk\ Images folder where N is the disk number for the sd card.

Log into the pi via ssh and run raspi-config to expand the file system,
set the hostname and so on.

Note that fing on my phone finds the new pi
better than the bthomehub finds it in Home Network (though that was
probably due to the static ip address I set for the Music Box tryout).

Check how much disk is used with

$ df -h

and remember ready for the upgrade step next.

Update and upgrade the install with

$ sudo apt-get update

$ sudo apt-get upgrade

If there isn't enough space for upgrade (it tells you before doing it),
then

$ sudo apt-get clean

will remove any old package archives and might free up enough.
Probably a good idea to reboot after this.

Install tightvncserver and my runner script with

$ sudo apt-get install tightvncserver

on the pi and

$ scp vncs.sh pi@piglowpi:/home/pi

on the mac in the same folder as this text file.

Configure git with

$ git config --global user.name "clivemjeffery"

$ git config --global user.email "clive@rosedene.com"

which set my github credentials, and

$ git config --global credential.helper cache

which will cache passwords for 1 hour (extended from default of 15 mins).
These require git version 1.7.10 and the latest wheezy has 1.7.10.4 so it
should work. It might also be good to set the line-ending behaviour with

$ git config --global core.autocrlf input

The same thing can be done on Windows with true as the argument. Even
better might be a per-repository setting in a .gitattributes file, see
https://help.github.com/articles/dealing-with-line-endings
Get a github project like qbike with

$ git clone https://github.com/clivemjeffery/qbike.git

# Some Python Utilities

$ sudo apt-get install -y python-setuptools

$ sudo apt-get install python-pip

# Dependencies for QBike

These are from Johannes Bader's blog at http://www.johannesbader.ch/2014/06/track-your-heartrate-on-raspberry-pi-with-ant/

Put in the USB ANT stick and 

$ lsusb

to check the vendor and product id. We're looking for Dnastream Innovations, Inc.
The data has been 0fcf:1009 (vendor:product) for both my Garmin and Suunto devices.

Create the udev rule that will make a usb node for the device.

$ ls /etc/udev/rules.d

To see what's there, then unplug the device and

$ sudo nano /etc/udev/rules.d/20-antplus.rules

to create the new rule file. The prefix numbers will order the rules setup by the daemon.

Plug it back in and check for a /dev/ttyUSB0 node that represents the ANT+ device.

Get python-ant (Johannes Bader's fork with the movestick fixes).

GOT UP TO HERE (DECIDE WHICH python-ant TO USE)

$ git clone https://github.com/baderj/python-ant.git
