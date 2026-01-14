---
title: I Rebuilt Chord Mage. Again. But Now It’s a Web Application
date: 2026-01-14 16:00:00
description: Why I rebuilt Chord Mage and what makes this version more open.
tags:
---
I know... I know. Rebuilt again? To be honest, I didn't expect it to happen, but I had to give in.

[Chord Mage](https://chordmage.com) is a project I started because I wanted to understand music theory and share my findings with other musicians.

The reason I built an app around it was to prove I could make an app, and it was a while since I did so. And it did work just fine.

But let's talk about the new version first.

## What's new in Chord Mage

Because it's a web application this time, you can open it anywhere you have a browser and internet. That is neat! No need to go to an app store to find and download it.

You'll find the application at: [https://chordmage.com](https://chordmage.com).

The application was given a new updated look and feel. You make progressions just as the mobile app would, but with a few extras.

1. There is now a **metronome** for you to play along with your progression
2. Set up the **time signature** you play in
3. Change the **BPM** of the backing track
4. Chord (and metronome) samples load on the spot

[![Chord Mage](chord-mage-screenshot.webp)](https://chordmage.com)

## Why the change?

In short: mobile app development and deployment is a lot harder than web development.

When I started Chord Mage I didn't really expect mobile development to be that much different from what I do from day to day. Which in theory is true, but in practise was a bit different.

I wasn't 100% at home in mobile app development, so I made the mistake of picking the wrong framework to work in to start with.

The second thing that I didn't really realise was that what I wanted to do with the app was not your run-of-the-mill type of app you'd want to build in a framework like React Native.

The moment I started implementing a metronome I ran into some issues with performance and very quick and time crucial triggering sounds.

This was fine, but quickly turned into a mess of me trying to work around the framework and hack my way to a solution for something that might have been better if I built it natively. And I didn't want to go down that rabbit hole.

So... I moved back to what I know best.

## Focus on the right thing

Doing this all in my free time and with the goal to learn more about music theory I thought it was smart to move away from what was holding me back and move to a way of working that doesn't require more time than needed.

And here it is. Easy to deploy and distribute. Easier to build. Focussed on learning music theory.

## Next up

While building this version I thought of a feature I want to add next. I want to create a sort of song book you can fill will songs and sheet music so you can practise songs and see the sheet music at the same time.

I am specifying the idea and the requirements and am going to see if I can add this feature soon. It would surely help myself with learning song for my guitar practise. I've had this idea as a separate application for a while, but it makes sense to try and integrate it into Chord Mage!

Cheers.
