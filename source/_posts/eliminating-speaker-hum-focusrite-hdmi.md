---
title: Eliminating Speaker Hum (Focusrite, USB-C, Yamaha HS5, and HDMI)
date: 2025-03-18 17:00:00
description: The hunt for a group loop hum in a Focusrite Scarlett 4i4, USB-C, Yamaha HS5, and HDMI setup.
---
I love making music. I love creating a space that inspires me to do so. I do not like cables, unclear specs, and unexplained hums.

![Focusrite Scarlett 4i4 and Yamaha HS5](./speaker.webp)

## Time to change my home recording setup

As some of you might know, I record and produce music at home from my home studio. I pride myself in having created a space where I can make music using semi-professional tools all by myself.

This does however come at a cost: a lot of devices, and a lot of cables.

More specifically: I am running a fairly simple setup.

- Focusrite Scarlett 4i4 interface.
- Shure SM7 microphone
- Yamaha HS5 monitors
- MacBook + Logic Pro

Nothing really fancy. But my desk (which I also work at) was starting to feel a bit crowded and served way too many purposes.

I wanted to move my music related stuff to another desk and connect my gear through a USB-C cable going from one desk to the other.

I also want to use HDMI to use an external display on the other desk for when I am using Logic Pro etc.

## Everything connected... and then there is a hum

Once I moved everything to the other desk and connected a USB-C cable to a hub, plugged in the interface, the monitor speakers, a synth, and an Arturia Minilab all seems alright.

![First setup](./diagram_1.webp)

The studio monitors where not being too weird, but there was a slight hum. Nothing crazy.

And then I connected the HDMI to my laptop. And a very loud hum came out of the monitor speakers. Damn.

## Debugging the hum

The first thing I tried **disconnecting all other devices** which were not used for music production. Sadly this did nothing for the hum.

Then to check if it had to do with using different outlet. So I connected **all power through the same outlet**. Didn't fix it.

I ripped the whole setup apart because I clearly had a problem in my new setup configuration.

![Second setup](./diagram_2.webp)

The hum started at the second I connected the HDMI cable to the laptop. Might it be **a faulty HDMI cable?** Nope!

Back to searching possible problems. And some of you might already have spotted something I could improve.

## External power supply for Focusrite Scarlett 4i4

Provided with the Focusrite Scarlett 4i4 is an external power supply. You can connect it apart from the data input to provide "clean" power.

This lifted a little bit of the noise, but certainly not enough. Maybe it solved just the ground hum and not the "other" hum. At least it improved a little bit.

## Balanced VS Unbalanced cables

When using music gear you'll be collecting a lot of cables to wire everything together. There are two types of cables used for connecting Yamaha HS5 speakers: balanced and unbalanced.

The difference between balanced and unbalanced is that the balanced cable also uses a part of the plug for ground. Since the Focusrite Scarlett 4i4 provides balanced outputs, I could simply hook up a TRS cable to the monitors.

![TRS vs TR](./trs.webp)

I switched out the TR to TR (normal mono audio) cables for TRS to XLR cables.

**And poof. Hum mostly gone.**

## Getting back to my new setup

I started putting the USB-C hub back in the mix. No problems so far.

And then I connected the Arturia Minilab MIDI keyboard back into the USB-C hub. **HUM!**

I didn't expect that at all! Strange enough the synth wasn't causing any problems.

The audio interface and MIDI keyboard were now **sharing the same USB-C hub**, and it caused problems.

## Solving the MIDI keyboard hum.

First thing I tried was to disconnect the audio interface from the music desk's USB-C hub and connect it to the one on the main desk. Still a hum.

Then I tried connecting the interface to another USB-C port on my MacBook, and the USB-C hub on another.

**Problem solved!**

## The final, practically noiseless, setup:

This process took me about two evenings to solve, and it gave me a lot of headaches.

![Final setup](./diagram_3.webp)

The result is that I am not running two separate (quite long) USB-C cables from the main desk to the music desk and an HDMI cable. All without any noticeable hum.

Going through the process step by step was helpful in pinpointing and solving the problems.

So if you ever find yourself in a hum situation try the following:

- Disconnect everything and connect one by one to isolate the source of the problem.
- Try a single power outlet for all devices.
- Use balanced audio cables (TRS / XLR).
- Use different USB-C ports for devices you want to isolate.

Hope this story might bring you some insight.

## UPDATE: This video might help too!

The day after I posted this, **loopop** published a video on YouTube detailing many ways how to get rid of hums. It's great! 

{% youtube 3asGhHUVO0o %}
