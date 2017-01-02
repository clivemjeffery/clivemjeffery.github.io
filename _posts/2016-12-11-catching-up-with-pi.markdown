---
layout: post
title: Catching up with Pi
---

## Reminder

It is really time to remember the way to find out if my CosyHutch processes are running.
~~~
ps axg | grep cosy
~~~
It seems that `cosycmd` is the one that falls over most. Must review the code.

## Updating and checking python gpio on old and new pis

sudo apt-get update
sudo apt-get install -y python3 python3-pip python-dev
sudo pip3 install rpi.gpio

Note pip3 on Raspian Wheezy is pip-3.2
Newest Raspian is Jessie (which *is* on the card in the Pi-nano) and that has pip3.

### The stepper motors are being difficult

No joy from ScratchGPIO7 or 7+ from simpleci - is it the Pi B rev 2?

Ideas:
* Check the GPIO is working with an LED or four and resistors
* Try a Pi1 - one of them must be (there's even a A about somewhere - I think)
* See if there's a way to test the motor controller HAT works (there was and it did)
* Get a new motor controller HAT? (i.e. one not soldered by me! But my bad soldering was fine...see below)


Yes it was the Pi B. Works on the rev 1 as before. That will do for now.

