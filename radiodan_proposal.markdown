Radiodan - A programmable internet radio
======================================================

What?
-----

We want to make a connected, physical IP radio, which anyone with basic web-programming skills can adapt to make interesting applications and interfaces.

Our goal is to improve existing code and documentation such that given a project proposal (e.g. 'a radio for a partially sighted person'), a small team can build a physical prototype within a week on cheap hardware. 

We plan to work in the open from the start, and Radiodan would be released as an open-source Ruby gem to encourage 3rd party effort and experimentation.


Why?
----

IRFS has worked with radio applications for several years, notably and successfully in collaboration with [Frontier Silicon and Global Radio on RadioDNS applications](http://www.bbc.co.uk/blogs/researchanddevelopment/2011/11/radiotag-wins-innovation-award.shtml) including ways to 'bookmark' radio programmes. Rapidly prototyping on radio hardware isn't really possible - for very good reasons - price and reliability are more important for production radio devices than ease of use for developers. Radiodan will allow us to quickly test and prune potentially interesting areas of radio research, which we can feed back into work with manufacturers and other organisations. 

Working in the open will allow us to test the hypothesis that if it was made easy enough to do, there would be a huge increase in creative ideas for radio. Making it simple for a large number of people is key. A rough analogy is 'view source' for radio: view source for the Web allowed anyone with a browser to see how to copy and change a webpage. View source for radio should allow anyone with Radiodan to see how to make something like it. 

Working in public will help us find people interested in this area from the start and incorporate their ideas into the documentation and underlying APIs.

As a starting point we aim to enable prototyping around topics such as the following:

* Second screen synced visual radio
* RadioTag with audio available on multiple devices
* Accessible radio
* Iterative testing of physical interfaces
* Personalised radio

The work links closely with work in BBC R&D on the Internet of Things, potentially enabling work with [Tangible Media-Affordances](http://www.bbc.co.uk/rd/events/tangible-media-affordances). It could lead to generalisations of the recent R&D work on [Perceptive Radio](http://wearemudlark.com/blog/the-perceptive-radio-a-project-for-bbc-rd/). It will enable and continue work on [Authentication for Connected Devices](http://www.bbc.co.uk/rd/blog/2013/03/authentication-for-connected-tvs), feed into architectural considerations around [egBox](http://www.bbc.co.uk/blogs/researchanddevelopment/2012/08/irfs-weeknotes-120.shtml), and could potentially involve developing and extending [RadioTAG](http://www.bbc.co.uk/blogs/researchanddevelopment/2011/09/radiotag.shtml) and other RadioDNS work. There are connections around R&D's [Universal Control API](http://www.bbc.co.uk/blogs/researchanddevelopment/2011/02/universal-control.shtml) for accessibility and orchestrated media, designed for TV but also more widely applicable to radio.


Technology and approach
-----------------------

Radiodan is currently a small Ruby server developed by Dan Nuttall that allows you to play BBC Radio Streams and other audio sources using [MPD](http://en.wikipedia.org/wiki/Music_Player_Daemon). Its usefulness lies in the ability to publish events which you can then subscribe to. For example, you can tell it to react to certain inputs (the example we used is to change stations following a button press), or tell it to emit data in response to other stimuli (e.g detect programme boundaries or track boundaries and send information about them). Initial experiments with the [Archers Avoider](http://planb.nicecupoftea.org/2013/04/16/archers-avoider/) have shown that it is straightforward to run and control Radiodan via a RaspberryPi or similar hardware. 

The work is planned to consist of

* defining initial applications that Radiodan should support
* developing APIs suitable for controlling the functionality
* consolidating the existing code to support easy installation on suitable hardware


Who?
----

The initial development stage would involve Dan and the apps team working in two closely-tied streams, over the course of one full sprint cycle.

1. Radiodan "Core" Development

    Dan is currently the sole developer of [Radiodan](http://github.com/pixelblend/radiodan). He has begun to abstract the core elements from his initial 10% time hacks into a software library that other projects can build from. He would spend the initial sprint finishing and documenting this work in order to produce a 1.0 release as a publicly available Ruby gem. The initial feature set of this would be heavily influenced by the prototypes being created in parallel by the rest of the team. 

2. Hardware / Software prototype built on Radiodan

    Andrew N, Dan and Libby would work on a simple prototype that exhibits the potential of a programmable radio device, creating a reproducible physical prototype of Radiodan. Dan has already begun some of the [work](https://github.com/pixelblend/radiodan_example) in 10% time. The aim is to allow a novice raspberry pi owner to setup, configure and run a Radiodan-powered BBC Radio device.

