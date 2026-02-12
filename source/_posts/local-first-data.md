---
title: "Local-First Data Storage: An Ode to the Browser" 
date: 2026-02-12 09:00:00
description: Do web apps always need a backend? Explore how IndexedDB enables local-first design, protects user privacy, and simplifies modern web development.
tags:
---
When using websites, web applications, or apps on our smart devices, we often have to sign up for an account before we are allowed to use the product.

Most of the time, the reason is that they need a way to store our data. But do they really need to?

I recently released a new feature for [Chord Mage](https://chordmage.com/songbook) where you can catalog songs you practise. _**And all this without a backend to store the data**_.

That's right. _**You probably do not need a backend for your application.**_

In this article, I want to challenge you to think local-first, rather than backend, cloud, or API first.

## Where does data live?

Data lives inside applications, on servers, in your browser, on your smart devices. It can be _short-lived_ or _persisted long-term_.

Sometimes data is only used while you're using an application and then gets removed once you close it. Sometimes applications store data for later use, like for instance your settings.

This persisted data can be stored in two different ways: locally or externally.

_**Locally**_ is when the data is being stored on the device where you are using the application on. For example, on your computer or your smart device.

_**Externally**_, or remotely, is when the data is being stored on another device. Be it through a backend service, API, or some sort of cloud. Your data is sent somewhere else to be stored.

## Do you need to store this?

Applications always handle some form of data. Whether it's running on a server somewhere, locally in the browser, or on a smart device.

One of the most important questions you can ask yourself is: _**"Do I need to store this?"**_

The simplest way to keep your application or service as privacy-friendly as possible is to ask this question with every piece of information you handle.

Do you really need to store the user's name? Do you really need to store their location?

What if this data were to leak? **It can't be leaked if it was never stored**.

This is the first step you can take towards improving what you store.

## Where do you store the data?

I love it when I can just jump into an application without signing up for an account. Use it for a bit and maybe decide later if I want to sign up.

More often than not, the services you sign up for would work perfectly without an account if most of the work were done by the browser.

Like I mentioned at the start of the article. [Chord Mage now has songbooks](https://chordmage.com/songbook). And the data entered by the user is never stored externally, but rather in the user's browser.

I do not need to store this data on my own servers. 

I do not need to own this data. 

And moreover, I do not risk of storing copyright-protected content added by the users.

## Concerns when storing data

You want data to be stored as securely and privately as possible. Data leaks are never great, and if you can prevent them by not storing certain information, then why not?

The EU has a lot of rules regarding storage of data. You must have heard of [GDPR](https://europa.eu/youreurope/business/dealing-with-customers/data-protection/data-protection-gdpr/index_en.htm).

Any platform which holds public data can be held accountable for what they host. What if your users start sharing copyrighted material or hateful content?

If you do not need to think about these concerns, then why would you?

## How to store data in the browser?

Most web developers have heard of or used [`localStorage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) to store simple key-value pairs.

While it's true that you can store more complex data through serialisation, it becomes a bit harder when working with relational data.

Luckily for us there is something called [`IndexedDB`](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) which serves as a database inside the browser.

You can see the different things stored inside your browser using the `Storage` tab of your inspector.

## Your browser has a database for you to use... so use it!

The API for `IndexedDB` is not the easiest to work with. Which is why I opted for [Dexie](https://dexie.org/) to have a nice layer between me and the browser database.

I can store relational data used in my application, such as songbooks, songs, and uploaded media.

My users can upload images, audio, and video files. All these get stored in rows in the `IndexedDB` tables I defined.

No need for backend communication and uploading files to a server over an internet connection. Everything is stored locally on the user's computer.

Pretty neat, right?!

Wouldn't it be great if all applications did the same and only store information on servers when it's needed?

## When would you store externally?

_But Gaya, if the data only lives locally, how do I access this information on other devices?_

That is the great thing: **you don't**. At least not automatically.

We're so used to our data being synced to the cloud that we forget how it even works in the first place.

You could create an export or save functionality to save the data to a file and have the option to import said data on another device.

Or you could make a sync option for people that wish to sign up. Making the sign-up and syncing of data optional, as an extra service.

## Why does this matter?

In this day and age we're very happy to give away our information to companies to do with as they please.

We've grown so used to signing up for everything and probably have hundreds of accounts for services we do not even use anymore.

Let's make the internet a bit better by taking a local-first and offline-first approach. 

By keeping the data locally I do not use any bandwidth. The experience for the user is super fast and the data is always on the user's computer.
