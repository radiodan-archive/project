# The Archers Avoider

### Libby Miller

People tend to listen to the radio by switching it on and leaving it on, while doing other things such as working, cooking, driving, housework and so on. What this means is that programmes people really don't like can be particularly jarring because they interrupt the pleasant background noise, so disrupt the other activity flow as well as being intrinsically annoying. 

The Archers is a very popular programme but tends to polarise people into those who love it (and the Archers is one of the unusual programmes on radio 4 where people tune in especially) and those who hate it, and consequently race to the radio to switch it off.

I'm one of that latter group.

So is our head of engineering, Sean.

In the R&D workshop on the Internet of Things, we decided to work on an idea that Sean had been thinking about for a while – an 'Archers Avoider' (alternate name “Barwick Obliterator” from the name of the theme tune, (Barwick Green)[http://en.wikipedia.org/wiki/Barwick_Green].

We took the 'racing to the radio' idea and decided to make a panic button that would immediately change radio stations if pressed, bringing instant relief from Pip's whining and Tom's business plans. 

Here's the idea in sketch form. I always find it very useful to try and draw how people will use it the thing we want to make, whether that's software or hardware or both:

![Archers Avoider usecase sketch](images/sketch.jpg)

## How we prototyped it

As with a lot of these ideas, a few things came together that would make it feasible to prototype in a couple of days:

* Working with FM / DAB radios and Arduinos is quite fiddly – I've tried it before without much success – but our colleague Dan already had working software that would play BBC radio stations over the internet, which is much easier to prototype with
* Jasmine and Cefn were on hand to help us with some of the electronics and the physical prototyping
* We had Raspberry Pis and shrimping.it to use plus lots of buttons, displays etc
* Sean and I had a genuine use for it, and a clear idea of what we wanted to make

Dan set me up with his software ('Radiodan'), helpfully available from (git)[https://github.com/pixelblend/radiodan.git]. We got it running on my Mac, and then set up the shrimping.it Arduino clone that Cefn helped us make attached to my machine via the USB port. Jasmine helped us wire up a button which sent a message over the serial port. So then all we had to do was create an interface between the serial port and Radiodan.

Radiodan is a Ruby-wrapper around the MPD audio player. Dan wrote a small utility for it that makes it switch channel streams for a specified number of seconds if a specific file has been changed: it checks every second if that's the case. So the button just had to change the file.

We tried a number of different ideas for interfacing with the Arduino clone. We tried (Noduino)[http://semu.github.io/noduino], but under time pressure I couldn't get it to work. Eventually Sean wrote some Ruby code that talked to the serial port via the Ruby serialport gem – you can see the code (here)[http://planb.nicecupoftea.org/2013/04/16/archers-avoider/] - most of the code and the time taken was handling 'bouncing' – a button push is actually quite a wobbly experience which needs to be translated into a binary one.

About 30 minutes before we had to do a demo, Cefn suggested trying it with a Raspberry Pi – and with a bit of help from him I got it working. It was a complete revelation how easy it was to use a Pi – I'd never tried it before despite owning one. With Raspian 'Wheezy' – a Debian OS for Raspberry Pi – we were on familiar apt-get install ground – and there are tons of libraries available for it.

We attached the shrimp to the Pi's USB port and it more-or-less just worked. The only fiddly bit really is finding out the IP address of the Pi, but the Mac's ability to share network via Ethernet made it simpler (you can usually tell the IP of an attached device via the console).

In a way the hardest part was making a robust and attractive case for it. Jasmine helped and Nikolaos joined us for a few hours to prototype a more advanced 'toaster' type interface, designed so that the farmer and sheep would gradually rise from the device and be batted down by the anxious listener in order to trigger the switch.

![Toaster physical prototype](images/toaster.jpg)

![Hackday prototype prototype](images/final.jpg)

This is the final version for the day. You can see the working big red button and a very nice Texas instruments magnifying display to show the current station.


## Next Steps

I spent a bit of time making it wireless – documented (on my blog here)[http://planb.nicecupoftea.org/2013/04/16/archers-avoider/] but the idea that's got me more interested is – what would it take so that anyone could make a customised radio like this? And that's the idea that we are exploring at the moment. 

Working with members of Bristol Hackspace and others, we're currently creating various applications of Radiodan – for example a time-travel radio that lets you go back to the previous day, a radio that speaks the name of the programme currently playing, or 'telly on the radio' that plays still images synced with an audio version of a TV programme. Using those prototypes, and working in the open with whoever is interested, we think we'll get a good idea of a simple kit and API that anyone with some html / javascript programming experience can use to make their own 'Wrong Radio'. 

The Archers Avoider itself needs more thinking about what would replace it (and how long for - does it need access to the scahedule?).

![Hackday prototype prototype](images/wrong_wradio.jpg)
