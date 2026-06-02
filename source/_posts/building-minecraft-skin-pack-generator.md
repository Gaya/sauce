---
title: Building a Minecraft Skin Pack Generator for Bedrock (compatible with The Hive)
date: 2026-06-02 09:00:00
description: I made a web app which can generate skin packs based on PNGs for Minecraft Bedrock players that are compatible with "The Hive"
tags:
---
It might sound like a lot of buzz words to attract Minecraft players, but I promise you it's not.

## TLDR;

I made a web app which can generate skin packs based on PNGs for Minecraft Bedrock players that are compatible with "The Hive"

You can see try the web app on: [https://mcskinner.netlify.app/](https://mcskinner.netlify.app/) 

## No more manual work

The idea for this application was not mine, but of one of the young people I guide at Bureau voor Pedagogiek.

He likes to create skins for Minecraft Bedrock with weird geometries and other quirky features.

I believe the tool he uses to draw these skins is [BlockBench](https://www.blockbench.net/).

The problem was that he'd have a lot of PNGs in the end and was manually crafty `json` files and what not to create skin packs.

There is some documentation by Microsoft on [packaging a skin pack](https://learn.microsoft.com/en-us/minecraft/creator/documents/packagingaskinpack?view=minecraft-bedrock-stable), but doing it all by hand seemed a bit overkill.

## What we made

Together we made a tool which:

- accepts PNGs
- allows adding a cape to the skin
- can import custom geometries to apply to skins
- makes animations of arms and legs changeable
- packs everything in a .ZIP file

When you're making a pack with a huge set of skins, this is a must-have.

## The result

Once we got it working by going back and forth testing the packs in Bedrock and a server called "The Hive" we finally landed on something which works.

See the outcome of the skin pack here. Follow this creator to see more!

{% youtube Cjj4sxdTink %}

## The hurdles

So this project didn't go as well as we hoped. It required us a couple of iterations before we could get these skin packs working in "The Hive."

There are some peculiar constraints to the JSON file for the geometries.

First is that almost all numbers inside geometries need to be a `float` / `double`, even when the value can also be an `integer`.

This means that, for instance:

```json
{
  "pivot": [0, 24, 0]  
}
```

Actually needs to be:

```json
{
  "pivot": [0.0, 24.0, 0.0]  
}
```

Both are valid JSON, but since `0.0` and `0` are essentially the same in JavaScript we don't really care.

This means that `JSON.stringify` converts `floats` into `integers` when they can be. Which also saves some bytes.

This resulted in some obscure steps I had to take.

## Forcing numbers to float in JSON

The first little hack I did was forcing `numbers` in JSON to become floats.

I did this by providing the following as a second argument to `JSON.stringify`.

```javascript
const data = JSON.stringify(
    mergedGeometry,
    (k, v) => {
      return Number.isInteger(v) 
        ? v.toFixed(1) : v;
    },
    2,
);
```

This code checks if the value (`v`) is an integer, if so, force it to a decimal notation.

I can hear you thinking: "but this turns it into a `string`!". Correct.

Which is why we need this little `RegExp` to fix the output:

```javascript
data.replaceAll(
  /"-?\d+\.0"/gm, 
  (s) => s.replaceAll('"', ''),
);
```

Look for all instances of quoted strings that have just a number in them (positive or negative) and remove those quotes.

So it will match:

```javascript
"-14.0"
```

And turns it into:

```javascript
-14.0
```

## Conclusion

All in all a nice idea with some fun implementations and things I never needed to make before.

You can view the source of the (mostly vibe coded UI) app here: [https://github.com/Gaya/McSkinner](https://github.com/Gaya/McSkinner)
