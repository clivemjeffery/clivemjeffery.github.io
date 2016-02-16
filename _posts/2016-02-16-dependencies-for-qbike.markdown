---
layout: post
---
These are the steps, very slightly adapted, that Johannes Bader set out the [post](http://www.johannesbader.ch/2014/06/track-your-heartrate-on-raspberry-pi-with-ant/)  that got me started.

### Register the ANT Stick

Insert the ANT stick and check the vendor and product id.

~~~
pi$ lsusb
~~~

We're looking for Dynastream Innovations, Inc and the preceding vendor : product combination. My Garmin ANT Stick is `0fcf:1009` and my Suunto Movestick Mini is `0fcf:1008`. I didn't realise they were different until everything stopped when I switched sticks. I eventually discovered the python-ant fork from Johannes is _hardcoded_ to the Suunto product id.

Create the udev rule that will make a usb node for the device. First, see what's there with.

~~~
pi$ ls /etc/udev/rules.d
~~~

Next, unplug the device and create the new rule file.

~~~
pi$ sudo nano /etc/udev/rules.d/20-antplus.rules
~~~

The prefix numbers control the order in which the rules are setup by the daemon. Plug the stick back in and check for a `/dev/ttyUSB0` node that represents the ANT+ device.

The remaining problem here is that `/dev/ttyUSB0` is only usable by root. I've looked through various permissons, group memberships (i.e. the `dialout` group) and other obscure settings - but haven't got the python program using the device as a *normal* user.

It is annoying because I'd like to test and develop via VNC with the pi running headless. Sor far I've not worked out how to combine starting `sudo ./qbike.py` while logged in to a VNC session (with tightvncserver). It must be possible, but there *are* some quick and dirty workarounds. 

### Python ANT

Get [python-ant](https://github.com/mvillalba/python-ant).

Johannes Bader said he had trouble with `AlternateSetting` and `Resource busy` errors and made a fork to fix them. So I tried [his fork](https://github.com/baderj/python-ant.git) and found the pre-installed raspian PyUSB library didn't include the `is_kernel_driver_active` function.

Commenting out Johannes' change in `python-ant` `/src` `/core` `/driver.py`, got everything working out in the shed with the Suunto stick, keyboard, mouse and screen attached. Back inside and running headless, I first got device not found errors (see the hardcoded product id issue noted above) and *then* the device busy errors. Could the pi kernel hold onto TTY interfaces when it runs headless but let them go when input devices are detected?

To get the `is_kernel_driver_active` function, you need to downgrade PyUSB to the b1 version of the package. These commands do the trick:

~~~
pi$ sudo pip uninstall -y pyusb
pi$ sudo pip install pyusb==1.0.0b1
~~~

~~~
pi$ git clone https://github.com/mvillalba/python-ant
~~~

Change into the new python-and directory and install the package.

~~~
pi$ sudo python setup.py install
~~~

Python [setuptools]() does a lot of work here and there are one or two warnings. Nevertheless, the package seems to build and install each time (even if edited).

Current status (date of post): qbike worked with the Suunto stick and without Johannes' `is_kernel_drive_active` patch. It doesn't work with the Garmin stick, hanging after printing `antnode created from stick`. Could be the PyUSB b1 package is now broken, could be the Garmin stick uses a different ANT+ key. I need to try the Suunto stick again but that's for another day.

### Get PyQtGraph

I use [PyQtGraph](http://www.pyqtgraph.org/), by Luke Campagnola, for the graph displays in qbike. It is build on [PyQt4](https://riverbankcomputing.com/software/pyqt/intro) which it will install as part of its dependencies. The first time I did this, I pulled a local copy of PyQtGraph into the qbike folder and added it to the `.gitignore` file. I was following the *most people* suggestion on the [install page](http://www.pyqtgraph.org/documentation/installation.html) and assumed this would protect qbike from getting way behind changes in PyQtGraph.

This time, I'll try a global system install, similar to the Python ANT one above. For fun, I tried the first method on Luke's install page. I edited the `/etc/apt/sources.list` file and then, after puzzling failures, found that you have to run `sudo apt-get update` before it will be able to find any packages in the new source.

Once it did, everything set up fine, `qbike.py` started up nicely (albeit only via `sudo` in a local desktop environment) and all the graphical widgets and graphs appear OK. This was quite a good way to set up for qbike because it installed all the other python Qt dependencies in one go.