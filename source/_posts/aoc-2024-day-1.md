---
title: Advent of Code 2024 - Day 1
date: 2024-12-02 16:00:00
description: Joining AoC 2024 again in TypeScript. Here are my findings of day one
tags:
---
I love [Advent of Code](https://adventofcode.com/) and I decided I'd join the event again this year. Last year I stopped at day seven as I think I might have been too busy. And like other years, each day will ramp up in difficulty, and I'll meet a point where I think the effort is to continue.

## What tools do I use?

It's quite simple to be fair. I code in TypeScript, test my code using Jest, and run everything with Node.js. It's the setup I've been using for a few years now, and it serves me well. No linting. No prettier. Just simple code.

You can find everything in my [AoC repository on GitHub](https://github.com/Gaya/aoc-2024).

I wrote a script that takes the puzzle inputs and the modules per day and runs them in succession. It keeps track of the time it costs to execute each day reports the results of the puzzle and the time it took to run.

I try to keep my solutions to under a second.

## Day 1 - Part One

The first problem we face in day 1 is to parse the input and create two sorted lists of numbers to compare.

Let's look at the code I wrote for parsing the input:

```typescript
const matches = input.match(/[0-9]+/gm);
```

This will go through the whole input string and grab the numbers.

```typescript
return matches
    .map((i: string) => parseInt(i, 10))
    .reduce((
      acc: [number[], number[]], 
      item: number, 
      index: number,
    ): [number[], number[]] => {
      return [
        index % 2 === 0 ? 
          [...acc[0], item]: acc[0],
        index % 2 === 1 ? 
          [...acc[1], item]: acc[1],
      ];
    }, [[], []]);
```

This piece of code is a bit more complicated. First I take the matches and parse the `string` to `number` by using a `map` function.

For the reduce function we're going to fill to separate arrays with number. `acc` holds two arrays, the left and right list respectively. Depending on the `index` we're going to put the number in the left or right array.

In order to solve part one we need to compare the left and right list and determine the distance between the numbers.

```typescript
const [a, b] = splitInput(input);

a.sort();
b.sort();

return a.reduce((acc, item, index) => {
  const distance = b[index] - item;

  return Math.abs(distance) + acc;
}, 0);
```

First we create the two lists of number, then we sort them. In JavaScript this means the source array will get modified, so we can just call it like line 3-4.

Then we quickly go over all the numbers in list `a` and compare the number to the number on the same position in list `b`.

`Math.abs` is a nice method to use to make any number a positive number. So for distance it would turn any negative distance (which is also a distance) into the positive equivalent. Reads a bit nicer than: `distance > 0 ? distance : distance * -1`.

## Day 1 - Part Two

As for part two. It's pretty simple. We get the same `a` and `b` lists.

```typescript
const scores = b.reduce((
  acc: Record<number, number>, 
  number,
): Record<number, number> => {
  acc[number] = acc[number] ? acc[number] + 1 : 1;
  return acc;
}, {})
```

We need to looks at the list on the right and determine how many times a number is on it in total.
This reduce will check all the numbers and add `1` everytime the number was already seen.
We will use this list as a quick reference for the next loop.

```typescript
return a.reduce((acc, item) => {
  if (!scores[item]) {
    return acc;
  }
    
  return (item * scores[item]) + acc;
}, 0);
```

Now for each number in `a` we'll first check if it exists on the right. If not, immediately return the current sum `acc`. And if found take the number in `a` and multiply it by how many times we saw it before.

## Conclusion

All in all a good start. Looking forward to the rest. I'll write about day two tomorrow. Cheers!
