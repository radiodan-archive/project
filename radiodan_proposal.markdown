Radiodan - A programmable internet radio
======================================================

What?
-----

Radiodan is a small ruby server that allows you to play BBC Radio Streams and other audio sources using [MPD](http://en.wikipedia.org/wiki/Music_Player_Daemon). Its usefulness lies in the ability to publish events which you can then subscribe to. So for example, you can tell it to react to certain inputs (the example we used is to change stations following a button press), or tell it to emit data in response to other stimuli (e.g detect programme boundaries or track boundaries and send information about them).

The potential of this is enormous. Radios, like TVs, are hard to prototype with. Their APIs are not available or undocumented, and even if documented are hard to use and inflexible. Even if APIs are available, the physical aspects of the radio are not controllable.

It *is* possible to create internet radio stream players of this sort, as Radiodan shows. The difference is that now we can relatively easily make a *stand-alone* internet radio for < £50 using a Raspberry Pi and various peripherals. This, combined with thoughtful API design should allow us to prototype around topics such as the following:

* Second screen synced visual radio
* RadioTag with audio available on multiple devices
* Accessible radio
* Iterative testing of physical interfaces
* Personalised radio

A reasonable goal is to get to the stage where, given a project proposal (e.g. 'a radio for a partially sighted person', a small team can build a prototype within a week on hardware like this. The radiodan project itself would be released as an open-source Ruby gem to encourage 3rd party effort in this area.

Why?
----

Don't underestimate how important it is for this stuff to be *easy*. Experimentation with hardware - getting to a point at which experimentation is even possible - is difficult for most people, and once that initial hurdle is breached, learning how to interact with hardware can be very time consuming. The massive development community around the Raspberry Pi has started to change that, and things are moving very fast.

There's no reason why this work shouldn't feed into e.g. fm or DAB radio work as well - it's just abstracting away from some of the difficult bits. It's also a step towards doing something like this for TV as well - we could learn from this to improve egbox's architecture.

Who?
----

The initial development stage would involve a team of three (Dan, Libby, Andrew N) working in three closely-tied streams, over the course of 1 full sprint cycle.

1. Radiodan "Core" Development
    Dan is currently the sole developer of  [Radiodan](http://github.com/pixelblend/radiodan). He has begun to abstract the core elements from his initial 10% time hacks into a software library that other projects can build from. He would spend the initial sprint finishing and documenting this work in order to produce a 1.0 release as a publicly available Ruby gem. The initial feature set of this would be heavily influenced by the prototypes being created in parallel by the rest of the team. 

2. Software prototypes built on Radiodan
  Andrew N and Libby would work on a simple prototype that exhibits the potential of a programmable radio device. Libby has produced an enormous list of possible applications for us to choose from. ** either paste here or link to separate confluence page **

3. Physical Prototype
  Libby and Dan would improve the [initial efforts](http://planb.nicecupoftea.org/2013/04/16/archers-avoider/) towards creating a reproducible physical prototype of radiodan. Dan has already begun some of the [work](https://github.com/pixelblend/radiodan_example) in 10% time.
  
  The aim is to allow a novice raspberry pi owner to setup, configure and run a radio-dan powered BBC Radio device. This would build upon the work in point 2.
