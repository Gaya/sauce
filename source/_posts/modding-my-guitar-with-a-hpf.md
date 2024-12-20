---
title: Modding my Guitar with a HPF
date: 2024-12-20 12:00:00
description: Modded my Yamaha Revstar RS620 a bit. Went from a coil split to implementing a high pass filter 
tags:
---

A while back I bought a second hand [Yamaha Revstar RS620](https://www.yamaha.com/en/about/experience/innovation-road/collection/detail/3083/) from a marketplace website. I fell in love with it, but there were a few things I wanted to change.

For starters, it could use a little love in terms of maintenance. The frets were a bit worn and the guitar could use a good setup. The bridge was also starting to rust and was damaged.

In terms of sound the guitar sounded very dark. It's not really the pickups fault, but rather the wiring and electronics that make it sound that way. It's lacking a bit in the top end.

There is also a "dry-switch" on the guitar. It filters out some of the low end and makes the guitar sound a bit more like a single coil. It's a nice feature, but I wanted to change it a coil split. Since I wanted the top end shine through I'd have to replace the "tone pot" of the guitar with a higher resistance value. So I could try to make a coil split in the process.

## The physical mods

I started with the physical mods. I wanted to replace the bridge, give the frets a good polish, and replace the knobs with speed knobs.

The bridge is replaced with a black [Gotoh 510UB](https://g-gotoh.com/product/510ub/?lang=en). The process was quite easy. All I had to do was remove the strings from the guitar. Remove the old bridge, which actually just slid off. Replace the bridge screws with the new ones and slide on the new bridge. A huge advantage of this bridge is that it locks in place and will not slide off when there are no strings on the guitar. Such a small thing, but makes a world of difference when restringing.

The knobs were the easiest. Just pull off the old ones and put on the new ones. I am not really sure if I want to keep these new speed knobs. They look a bit better, but feel a bit cheap and plasticky.

Here is the end result: Before / After.

![Replaced bridge and knobs](before-after.webp)

## The electronics

I started with the coil split. I replaced the tone pot with a 500kΩ push-push potentiometer. I also replaced the stock capacitor with a 0.047μF capacitor. This is the standard value for a coil split.

I followed a wiring diagram I found on [Seymour Duncan's wiring diagrams section](https://www.seymourduncan.com/resources/pickup/wiring-diagrams) and wired up the internals to match that of a two humbucker coil split setup.

When I tried the coil split I was very underwhelmed. It sounded very weird, as if I was listening to my guitar signal through an AM radio. Very boxy and thin sounding. It was not just the low-end which was missing, it just sounded very off.

I did however really like the "dry-switch" the guitar had originally. So I thought about bringing it back. This meant I had to remove the coil split. Wire up everything to almost the original circuit and add a high pass filter to the push-push potentiometer.

## What is a high pass filter? And how does a guitar pickup work?

In a nutshell electric guitars work very simple. The strings vibrate and create a magnetic field. This magnetic field is picked up by the magnets in a  pickup and turned into an electric signal. This signal is then sent through the guitar's components (volume and tone knobs) and then to the output socket.

All an amplifier does is pick up this signal and amplify it. The signal is then sent to a speaker which vibrates and creates sound.

This is however a very basic explanation, but I don't need to go into more detail for this post.

A high pass filter (HPF) will take this signal and cut off the low frequencies of the sound. This means it will remove the bass frequencies from the signal while maintaining the higher frequencies.

![HPF circuit](circuit.png)

I looked up a basic scheme and saw that it's actually super simple. I just needed a capacitor and a resistor. I had a 10μF capacitor and a bunch of resistors, so I could figure something out here.

## Testing and implementing the circuit

How did I land on these values? I didn't. I just looked at the existing circuit and kind of guessed some of the values. Then I created a breadboard setup with two jack sockets to test out the circuit on the fly.

![Testing circuit on a breadboard](breadboard.webp)

This allowed me to swap out components and see (hear) the effect it had on the sound. I opened up an EQ on my computer to also see the effect in action. When I was happy with what I heard I started re-soldering the components in my guitar to match the breadboard setup.

A push-push potentiometer allows me to switch the HPF on and off. This way I can switch between the original sound and the modified sound. I had to replicate the breadboard design on just a tiny part of the guitar's circuit. And with just two components it was quite easy to do.

![Soldering the components in place](soldering-hpf.webp)

## The end result

I am quite happy with the looks of the guitar. Might swap out the knobs, but that's not really important. The bridge is a nice upgrade and the polished frets look and feel great.

The sound is also much better. The HPF really makes the guitar sound a lot brighter. It's not as dark as it was before. Also without the HPF engaged the pickups sound a lot more open and clear.

I might take another look at the circuit later and actually do the math to figure out the correct components.
