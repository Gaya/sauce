---
title: I Was Wrong About NativeScript
date: 2025-05-12 19:00:00
description: Why I pivoted from NativeScript to Expo + React Native after launching my app. Lessons learned, pitfalls faced, and how I rebuilt fast and better.
tags:
---
A couple of weeks ago I launched my app [Chord Mage](https://chordmage.com) and with it wrote about how I went [from idea to app in a week](/from-idea-to-app-in-a-week).

Here I talked about the fact that I picked NativeScript as it seemed like a solid choice at the time. 

I am back to tell you that I went in a different direction. Why I re-wrote my app in a week. 

*TLDR: I went with Expo + React Native.*

## Another framework?

Yes. [Expo](https://docs.expo.dev/) specifically. Which is an ecosystem (as they call it themselves) to make development using React Native easier.

I had already used the framework and liked it... but it was far from perfect back then. When I came across *NativeScript* not to long ago it felt like NativeScript were doing things just a bit better than I remembered Expo to be.

When I was building the app with NativeScript I did run into some things, but *the setup and getting started guide worked so well* I was kind of impressed.

In my haste, or eagerness, or enthusiasm, I picked NativeScript and just went with it.

## So what went wrong with NativeScript?

The framework in itself is not really bad, but there were some **assumptions** which I made which didn't turn out to be true. 

First of all. And maybe the stupidest of all assumptions was that it was built on top of React Native, like Expo would be. *Wrong*. Clearly inspired by, but not built on top of. It's its own kind of implementation of React and JavaScript to native.

Looking back at the documentation now, I have no clue how I missed that fact, but I assumed I could just drop in React Native modules whenever I'd want in the future. I was wrong here.

While that is not a huge problem, I quickly found that modules for `react-nativescript` were not as up-to-date as I was used to. Because NativeScript supports all sorts of JavaScript frameworks, I understand it's a lot of work keeping them all up to date, and support each one.

This meant that support was not as recent as I had hoped. And it showed in the sloppy way I was making the app.

## Rendering and other quirks

One of my biggest struggles with NativeScript was that the rendering was often times a bit weird. Sometimes state updates *wouldn't propagate* properly. Sometimes updates just plainly *broke* the layouts. And in some weird cases it made the layout be *re-ordered and plain wrong*.

I remembered React Native having these sort quirks too and kind of wrote it off as "not fixed yet" and started implementing some workarounds and weird tricks to solve the issues. For instance by updating and setting `key`s on components to force React to view them as different components each render, where they would normally not really need it.

Styling elements of the app was also *a bit different* from what I'd expect, but that's forgivable. It was like *re-learning CSS* sometimes.

The development server and updating the app wasn't that great either, but I could live with that. Sometimes components updated on the fly, and sometimes the whole app refreshed. This was not a huge problem though. But I learned later this could be massively improved.

## The good parts of NativeScript?

Building and running the app is great. Their support for getting started and running your project in iOS simulators and the Android emulator is great. I really have to give NativeScript the win on this one.

## You just wrote the app, why re-write now?

Just as I started to implement new features I quickly learned that NativeScript was in fact *not based* on React Native. This made it a bit harder to make use of React Navigation modals among other things. It was all *just* not there. Very annoying to be honest. And it started to bug me.

So I had the choice to either fix the stuff in NativeScript *or* switch to a more maintained framework. I was constantly making my own implementations and workarounds for things, and that's something I'd rather use modules for.

Since the main logic was *written in React already*, it would not be too hard to re-write it to React Native's components. I'd have to probably re-style some things, but **the flow and logic would be the same**.

That's when I started looking around and stumbled into Expo again. *Fine*. I'll give it another try.

And boy was I happily surprised.

## Giant leaps forward

What I immediately noticed that the sample code for Expo projects looked way more up-to-date with the standards I wanted to use.

Expo and React Native also have **a lot of components and modules** ready for you to use, and that is great. I didn't realise how many thing I made myself until I started converting the app to React Native and found pre-made solutions to problems I just solved, and much better too!

I also noticed that the update process of React Native felt very different from what I remembered. There seems to be less focus on the platform specific build folders like there was before. That's what I liked about NativeScript too.

## The not so good parts

While the setup process was not as easy as NativeScript's, I got setup pretty quickly. One of the main drawbacks of Expo is that they really, really, want you to use their EAS system. A sort of service which builds your app for you.

I really like building things on my own machine and not be dependant of external services. It might be great in a team setting, but I'd like my own workstation to handle things.

In my opinion Expo gives the developer too many options and flavours here. I'd go full EAS or full local, not some in-between option.

## Re-write

I had most of my components ready to be re-written. Just a couple of things I had to figure out were:

For i18n, I went with `react-i18next`. It's pretty straight forward and works great in React Native.

Navigation is solved using `react-navigation`. I didn't go with Expo's file system based navigation as it tends to not as ideal and not as flexible as declarative routes.

I had to redo a lot of layout components to be flex based, but that actually made the code and layout logic a lot easier. I didn't notice a drop in performance, if anything everything *feels smoother* now.

## Now what?

This means that right now I have the basis for moving forward a bit better. And I am glad I did it right now and not later.

Do not be afraid to pivot your stack this early in the life of your products.

I often times say:

> Build it once. Then build it good.

And this time I listened to my own advice.
