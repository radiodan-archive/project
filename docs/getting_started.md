Radiodan is a piece of software that lets you build your own internet radio. 

This site explains how to set it up on a Raspberry Pi with some BBC streams, but it is easy to use with other 
streams, and MP3 files and other audio formats. It uses Ruby code on top of MPD.

We've made it because we are interested in different kinds of physical radio devices and how we might change 
their functionality to make them better. We think that you can only test this by building radio-like devices, and 
the more people who can build them, the more interesting the radios will be.


Things you will need
====================

A wifi connection - it can be open or password protected (WPA or WEP) but this won't work if it's a captive 
portal where you have to go through a web page to get connected.

An SD card reader - computer commonly have them built in, or they can be bought very cheaply.

A computer suitable for putting data on the SD card - Windows, Linux or Mac OS X

Raspberry Pi

The Raspberry Pi is a small, cheap computer with an ethernet port, two USB ports, audio out and HDMI out. It 
doesn't come with a keyboard, monitor, mouse or harddrive - it's powered from an SD card of the kind you get in 
cameras. You can buy them from Farnell or @@

SD Card

Get a 4GB or higher 10-speed card like this one@@. It can be a mini SD card with an adaptor, like this one@@.

Speaker

Anything with a standard jack will do. There are some very cheap tiny speakers available, such as this one@@.

Wifi card - get one with @@ chipset, like this one

USB hub@@

USB extender cable@@

USB to mini-USB cable@@

USB plug, like this one@@

A box to put it in

An LED like this one@@. Strictly speaking you could do without this, but it makes things much easier to have it.


The approximate cost should be about £60.

Optional

* A soundcard, like this one@@, in which case you might need a USB extender
* One button and two rotary encoders, wire, spade connectors and some crimpers (see @@below). You can do without these but it's more fun if you have physical buttons and dials for your radio.
* Keyboard, mouse, monitor. You don't need these to set it up, though if somethng goes wrong it might be helpful 
to have them.


Getting started
===============

1. Download this @@SD Card image

This is a custom image that we have created from 
- [Raspian Wheezy image](http://downloads.raspberrypi.org/raspbian_latest)(zip)
- [Radiodan cold_start](https://github.com/radiodan/cold_start) (github link) which includes
-- [radiodan](https://github.com/pixelblend/radiodan) (github link)
-- [radiodan_example](https://github.com/radiodan/radiodan_example) (github link)

2. Put the image on the SD card using the SD card reader
- Raspberry Pi have [instructions here](http://www.raspberrypi.org/wp-content/uploads/2012/04/quick-start-guide-v2_1.pdf) (pdf)
- if you are comfortable using dd on linux of Mac OS X you can just do:

    diskutil list
    # insert SD card

    diskutil list

    # identify your SD card as the new one
    # where 'n' is a number
    diskutil unmountDisk /dev/diskn

    # Downloads/ is whereever it downloaded to
    dd bs=1m of=/dev/disk2 if=~/Downloads/radiodn_0.1.img

3. Eject the disk from your SD card reader and assemble the components, like this:

@@include an led
 

4. Turn the Pi on and attach it to the wifi

In about 1 - 2 minutes you should see the led light up and flash green@@. When this happens, on your main 
computer, look for a new wifi network called "radiodan-configuration'. Join this network, and you should see a 
web page pop up (like a 'captive portal' you get in some wifi networks). Follow the instructions and select a 
wifi network to connect to and give it the password. Click 'reboot now', and rejoin your usual wifi network.

5. Listen to the radio

If all that has worked, 1 - 2 minutes after the reboot, you should hear Radio 1 playing.

6. Control it using the webpage

You can control your radio by adding buttons and dials (see below@@), but also by going to 

http://raspberrypi.local:3000

in a web browser when you are on the same wifi network as your radiodan.


What's happening under the hood
===============================

The image we have created uses cold_start to remove some of the packages that come with Raspbian, in order to make 
the image as small as possible. This includes all of the Desktop packages, so that if you want to programme it later 
you'll have to use the command line.

It also sets up two programmes to run on startup
* cold_start wifi setup
* radiodan_example app runner

The wifi setup scans the environment for networks and then makes itself a wifi access point. This means that you 
can connect to it using another computer and set it up in a web page, as described above.

The app runner looks for applications in the /home/pi/apps/ folder and if they have a Procfile, attempts to 
install all their Ruby dependencies (using bundler) and then uses upstart to ensure that they start when the 
machine is booted.


Adding buttons and dials
========================

If you've got this far, you should be able to control your radio using its webpage, but it's much more fun to wire 
up some physical buttons to make it more like a real radio.

For this you will need:

* Two rotary encoders with matching dials, like these@@. Get ones with a screw-in part to fix them to the box.
* A clicky button, for example this one@@, again, find ou=ne that you can screwe to your box.
* Some jumper wire. Easiest is to get male to female, like [this](http://www.tandyonline.co.uk/male-to-female-jumper-wires-10pk.html)
* Spade connectors suitable for your buttons and also for your rotary encoders@@. For example these@@. These are just a way for you to connect your buttons to your Pi without soldering. 
* A crimper, like this one@@ (you may be able to make do with pliars, but I wouldn't recommend it), to join your spade connectors with your wire.













