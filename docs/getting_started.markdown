Radiodan is a piece of software that lets you build your own internet radio. 

This site explains how to set it up on a Raspberry Pi with some BBC streams, but it is easy to use with other 
streams, and to add MP3 files (and other audio formats). It uses Ruby code on top of [MPD](http://www.musicpd.org).

We've made it because we are interested in different kinds of physical radio devices and how we might change 
their functionality to make them better. We think that it's only possible to test what makes a radio better by 
building devices that act like radios, and that the more people who can build them, the more interesting the 
radios will be.


Things you will need
====================

* An [SD card reader](https://www.google.co.uk/search?q=SD+card+reader) - computers sometimes have them built in, or they can be bought very cheaply.
* A computer suitable for putting data on the SD card - Windows, Linux or Mac OS X.
* A wifi connection - it can be open or password protected (WPA or WEP), but our cold_start proceedure which links the Raspberry PI to a wifi network won't work if it's a captive portal where you have to go through a web page to get connected. It also won't work with proxies at the moment.
* A [Raspberry Pi](http://www.raspberrypi.org). The Raspberry Pi is a small, cheap computer with an ethernet port, two USB ports, audio and video. It doesn't come with a keyboard, monitor, mouse or hard drive - it's powered from an SD card of the kind you get in cameras. You can buy Pis from [Farnell](http://export.farnell.com/rp/order/) or [RS](http://uk.rs-online.com/web/generalDisplay.html?id=raspberrypi)
* An SD Card - get a 4GB (or larger) class 10 card [like this one](http://www.dabs.com/products/sandisk-ultra-secure-16gb-sd-card---30mb-s---class-10---sdhc-uhs-i-89F3.html?refs=57120000&src=2). It's quite hard to find standard cards smaller than 16GB, so you could use a [micro SD card](http://www.dabs.com/products/kingston-microsd-4gb-class-10-memory-card---adaptor-not-included-7MBL.html) (but remember to buy [an adaptor, like this one](http://www.amazon.co.uk/MICRO-SD-TO-CARD-ADAPTOR/dp/B0019AJJRK))
* A speaker. Anything with a standard jack will do. There are some very cheap tiny speakers available, [such as this one](http://www.amazon.co.uk/Veho-Rechargeable-Speaker-iPods-Players/dp/B002CS2T4I/ref=sr_1_1).
* A  USB Wifi card - it's important to get one with the *RT5370 chipset*, like [this](http://www.ebay.co.uk/itm/WIFI-150MBPS-WIRELESS-ADAPTOR-802-11-B-G-N-LAN-NETWORK-MINI-USB-DONGLE-ADAPTER-/321023374826?_trksid=p2054897.l4275) or [this](http://www.ebay.co.uk/itm/Mini-150Mbps-150M-USB-2-0-WiFi-Wireless-LAN-Network-Card-802-11-n-g-b-Adapter-/120912927894?_trksid=p2054897.l4276)
* A [USB hub](https://www.google.co.uk/search?q=usb+hub), which doesn't have to be powered
* A USB extender cable, approximately 2 metres long, for example [this one](http://www.amazon.co.uk/Plug-Socket-Extension-Cable-Speed/dp/B00077DJK4/ref=sr_1_1)
* A [USB to mini-USB cable](http://www.amazon.co.uk/female-Micro-male-Cable-Adapter/dp/B005GI2VMG/ref=sr_1_4)
* A USB mains plug [like this one](http://www.amazon.co.uk/ADAPTER-CHARGER-BLACKBERRY-SAMSUNG-TOMTOM/dp/B00CLR00JQ/ref=sr_1_1)
* A box to put it in, a cardboard one is good. We have made some [templates](box_design.markdown) for you to try, or you could use an old [teabag box](http://www.flickr.com/photos/nicecupoftea/9564907822/in/set-72157635210928095) or something similar.


The approximate cost should be about £60.

Optional

* A [soundcard, like this one](http://www.amazon.co.uk/USB2-0-External-Quality-Channel-Adapter/dp/B003ZM0XIY/ref=sr_1_2), in which case you might need a [small USB extender](http://www.amazon.co.uk/Ex-Pro®-Professional-Cable-Female-Extension/dp/B007VDR0F2/ref=sr_1_1) - you'll need to [configure the sound card manually](https://gist.github.com/andrewn/6352695)
* Four [buttons](http://www.coolcomponents.co.uk/switch-mini-tactile-pcb.html) and [one rotary encoder](http://www.coolcomponents.co.uk/rotary-encoder-illuminated-rgb.html) with [dials](http://www.coolcomponents.co.uk/clear-plastic-knob.html), [jumper wire](http://www.tandyonline.co.uk/male-to-female-jumper-wires-10pk.html), [spade connectors](http://www.maplin.co.uk/miniature-female-spade-connector10-pack-34145) and [crimpers](http://www.rapidonline.com/Cables-Connectors/Crimp-Tool-Kit-Re-85-0270/?sid=e5a5a13e-681b-4dd6-a9ba-b0179034f95c) (see [below](#buttons)). You can do without these but it's more fun if you have physical buttons and dials for your radio.
* Keyboard, mouse, monitor. You don't need these to set it up, though if something goes wrong it might be helpful to have them.


Getting started
===============

## 1. Download [this SD Card image](http://dev.notu.be/2013/12/radiodan/radiodan2.zip) (580MB zip)

This is a custom image that we have created from 

* [Raspian Wheezy image, 2013-09-10](http://downloads.raspberrypi.org/raspbian/images/raspbian-2013-09-16/2013-09-10-wheezy-raspbian.zip) (zip)
* [Radiodan cold_start](https://github.com/radiodan/cold_start) which includes [radiodan](https://github.com/pixelblend/radiodan) and [radiodan_example](https://github.com/radiodan/radiodan_example) and [radiodan_example](https://github.com/radiodan/radiodan_example_physical_interface) (github links)

We chose the slightly older 2013-09-10 Raspian image because we wanted to keep it small, and we make a lot of updates to it anyway.

## 2. Put the image on the SD card using the SD card reader

Raspberry Pi have [instructions here](http://www.raspberrypi.org/wp-content/uploads/2012/04/quick-start-guide-v2_1.pdf) (pdf). If you are comfortable using dd on linux or Mac OS X you can just do:

    # list the disks
    diskutil list
    # insert SD card
    diskutil list
    # identify your SD card as the new one
    # where 'n' is a number
    diskutil unmountDisk /dev/diskn
    # Downloads/ is wherever it downloaded to
    dd bs=1m of=/dev/disk2 if=~/Downloads/radiodn_0.1.img

## 3. Eject the disk from your SD card reader and assemble the components, like this:

<img src="assets/pi_components.jpg" alt= "cables layout" width="600"/>

## 4. Turn the Pi on and attach it to the wifi

In about 1 - 2 minutes you should see a new wifi network called 'radiodan-configuration'.

Join this network, and go to a web page (or if you are on a Mac you should see a web page pop up, like a 'captive portal' you get with some wifi networks). 
Follow the instructions and select a wifi network to connect to and type in the password. Click 'reboot now', and 
rejoin your usual wifi network.

## 5. Listen to the radio

If all that has worked, 1 - 2 minutes after the reboot, you should hear Radio 1 playing.

## 6. Control it using the webpage

You can control your radio by adding buttons and dials (see [below](#buttons)), but also by going to 

http://raspberrypi.local:3000

in a web browser when you are on the same wifi network as your radiodan.


What's happening under the hood
===============================

The image we have created uses cold_start to remove some of the packages that come with Raspbian, in order to make 
the image as small as possible. This includes all of the Desktop packages, so that if you want to programme it later 
you'll have to use the command line.

It also sets up three programmes to run on startup
* cold_start wifi setup
* app runner

The wifi setup scans the environment for networks and then makes itself a wifi access point. This means that you 
can connect to it using another computer and set it up in a web page, as described above.

The app runner looks for Ruby applications in the /home/pi/apps/ folder and if they have a [Procfile](http://ddollar.github.io/foreman/), attempts to 
install all their Ruby dependencies (using [bundler](http://bundler.io)) and then uses [Upstart](http://upstart.ubuntu.com) to ensure that they start when the 
machine is booted. Two are included - [radiodan_example](https://github.com/radiodan/radiodan_example) and [radiodan_example_physical_interface](https://github.com/radiodan/radiodan_example_physical_interface)


<a name="buttons"></a>
Adding buttons and dials
========================

If you've got this far, you should be able to control your radio using its built-in webpage, but it's much more 
fun to wire up some physical buttons to make it more like a real radio.

For this you will need:

* One [rotary encoder](http://www.coolcomponents.co.uk/rotary-encoder-illuminated-rgb.html) with a [knob](http://www.coolcomponents.co.uk/clear-plastic-knob.html). Get ones with a screw-in part to fix them to the box.
* Some clicky buttons, for example [these](http://www.coolcomponents.co.uk/switch-mini-tactile-pcb.html), again, it's best if you can find one that you can screw to your box. The clickiness gives better feedback to the person clicking it that it's been pushed correctly.
* Some jumper wire. Easiest is to get male to female, like [this](http://www.tandyonline.co.uk/male-to-female-jumper-wires-10pk.html)
* Spade connectors suitable for your buttons and also for your rotary encoders. For example [these](http://www.maplin.co.uk/miniature-female-spade-connector10-pack-34145) - check that they are the correct size for your button's connectors. These are just a way for you to connect your buttons to your Pi without soldering. You could also use crocodile clips.
* A crimper, [like this one](http://www.rapidonline.com/Cables-Connectors/Crimp-Tool-Kit-Re-85-0270/?sid=e5a5a13e-681b-4dd6-a9ba-b0179034f95c) (you may be able to make do with pliers, but I wouldn't recommend it), to join your spade connectors to your jumper wire.

Assemble everything according to this diagram:

<a href="assets/Radiodan_app.fzz"><img src="assets/Radiodan_app.png" alt="Fritzing diagram"/></a>
 
