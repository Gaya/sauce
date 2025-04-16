---
title: From Idea to App in a Week - Meet Chord Mage!
date: 2025-04-08 10:00:00
description: A practical guide to building and launching a web app in just one week. Covers idea validation, rapid development, scope management, and learning from real user feedback.
tags:
---

Just two weeks I back I got an idea to build an app. And with the tools and knowledge I have to my disposal... I just thought: Let's build it.

How does building an app from scratch work in 2025, and which things did I run into?

Let me take you through all the step I took and the problems I faced along the way.

So. Meet [Chord Mage](https://chordmage.com).

[![Chord Mage](intro-image.webp)](https://chordmage.com)

## The idea.

As I have been learning guitar for the past year I've been dipping my toes into getting to know music theory a better.

The advertisement gods have picked up on that and started to bombard me with ads for a chord progression helper tool.

I took a closer look at what the tool was offering, and thought: isn't it way easier to understand if this was an app?

The layout of the tool is kind of confusing, and frankly quite expensive for what it is. So I had to make it.

## What to use?

At first, I thought of creating a simple web based application for this, but since I already know how to do such a thing and always want to learn new stuff, I decided it was a great idea to launch a new app into the world.

This meant I'd have to deal with iOS and Android. I remember iOS development being a pretty seamless experience, Android on the other hand, made me worry a bit.

I decided I needed a platform which supports both iOS and Android, and was not very hard to use. Also... I didn't have the time to learn a completely new programming language. So it had to be one I knew.

In the past I used React Native with Expo. But I wasn't really fond of their upgrade strategy. I could do with a platform with a little more opinions and less freedom. I wasn't going to build anything groundbreaking.

After a bit of research I stumbled upon the project [NativeScript](https://nativescript.org/) which allows you to write your app in not only JavaScript and TypeScript, but also supports an array of different frameworks.

## Why NativeScript?

What really spoke to me was that they basically created a layer on top of existing native platforms. It would create a programming interface I could work with, while offering a native experience for the end user.

You might think: "But doesn't React Native do this?". In a way: yes. But in this case NativeScript offers a lot more.

Apart from a bunch of components to work with, it comes with a lot of tooling around development and deployment. 

One of the things I least liked about React Native and Expo was the fact that upgrades could cause changes in how xcode and Android projects worked. It often times needed a lot of refactoring. NativeScript offers a sort of scaffolding way of managing project settings. Perfect.

Everything felt so streamlined compared to with what I was used to. Sure it has its quirks, but that could be overlooked for the actual pains it is solving.

From a complete fresh install I was up and running developing the app in an iOS simulator in just one hour. I didn't even have xcode or any simulator installed!

## Music theory and chord progressions

Ah, yes. Music theory. It's fascinating. What makes notes sound good together, and why? It is something I really wish to understand better.

The thing with music theory is that it happens to work in a strange mathematical way. Which is actually perfect for us programming nerds.

The app I wanted to create would make creating chord progressions a bit easier. It's based on the [IV-V-I progression](https://en.wikipedia.org/wiki/I%E2%80%93IV%E2%80%93V%E2%80%93I) with some extra modes to work with.

I will spare you the details, as I am not really the right person to be explaining why the theory works. I just implemented what I saw.

Here is a short introduction to what the app does:

{% youtube 8kb-UJYvHkA %}

## The biggest hurdles

It wasn't so much the actual development, but the release process that takes up a lot of time. It's good for me to run this whole process through again, but boy, is it cumbersome.

Getting the app on the App Store was not that difficult. I have to say the process is pretty clear and using NativeScript made it a bit easier. Most of my time was spent setting the app up and getting everything in order before it could be sent in for review.

I think the hardest part of the iOS development and release was figuring out TestFlight and App Store Connect, but honestly. Not bad.

Then came the next platform. Android. Which I own zero devices with of. So I had to find someone with an old device. As it happens my mom had an old Samsung S9 lying around. Nice!

But before I got the device I wanted to see if I could run it in an emulator. Which I remembered to be an awful experience. Luckily though, the Android development and emulation cycle has been greatly revamped since I last built an app. I was honestly surprised at how fast I had a working emulator with my app running in it.

As a bonus, the app didn't even need that much work.

## Download now

You can find Chord Mage on the [App Store](https://apps.apple.com/us/app/chordmage/id6743616312?platform=iphone) and [Google Play](https://play.google.com/store/apps/details?id=com.theclevernode.chordmage).

For more information check out [chordmage.com](https://chordmage.com)

## What's next

I wish to expand the functionality of the app pretty soon, as well as improve support for it.

Expect some more in-depth mobile development articles as well.

Cheers.
