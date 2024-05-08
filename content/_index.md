+++
title = 'Intro'
draft = false
+++

FIXME: while all of this information should be interesting, some of it should probably eventually be split out to other pages.

## What is voorkant?

voorkant is a (set of) frontends for Home Assistant, built outside of your web browser, aimed at devices too weak to run a web browser.
voorkant is written in C++ for performance and portability, using libcurl (currently) to talk to Home Assistant via a websocket connection - which means everything is live, there is no polling.

## Why is it called voorkant?

[_voorkant_ is the Dutch word for _front_](https://en.wiktionary.org/wiki/voorkant) or _front side_.

## Can I see some pictures?

Check out our [screenshots page](/screenshots).

## What frontends does voorkant provide?

We currently ship three frontends:

* `cli` -
  a commandline tool for interacting with HA from your shell prompt.
  Run commands, list your entities, subscribe to state changes.
* `ftxui` -
  a terminal UI that allows viewing entity states and invoking calls on them.
  This was built to test our HA interactions before we had an actual GUI, but it is useful by itself too.
* `LVGL` -
  the current focus of the project.
  This is a graphical interface that can run in a window on your PC, but can also run on various embedded (Linux) devices with touch screens (or perhaps, in the future, also some without!).
  It also works on the framebuffer console of your Raspberry Pi, if you can figure out how to input touches/clicks.

## Why did you build voorkant?

("I" is Peter).

I have an Eneco Toon 2 thermostat, rooted thanks to [ToonSoftwareCollective](https://github.com/ToonSoftwareCollective), with their "app store".
This is a fine device that responds well to screen touches.
I was missing a few features/apps that would be nice to have, so I bought a Toon 1 to do app development on.
It turns out that Eneco/Quby's stock software on a Toon 1 is unbearably laggy.
I wondered if the hardware really was that bad, or if the software was just inefficient, so I tried a few things, and soon realised that [it could run Doom](https://fosstodon.org/@habbie/110141084306659319).
This suggested to me that the existing software was not showing the full potential of the hardware.

Looking around for suitable GUI libraries, I found LVGL.
Porting the LVGL demo showed that this device could be quite responsive with the right software, so I decided to write a native Home Assistant client for the device.
And so, voorkant was born.

## Who built voorkant?

voorkant was originally thought up by [Peter van Dijk](https://github.com/Habbie), who wrote the first few lines of code.
Once it started taking shape, [Ruben d'Arco](https://github.com/cyclops1982) joined in and contributed big chunks of work.

Day zero enthusiast [Robert van der Meulen](https://github.com/rvdm) provided valuable input on many topics.
