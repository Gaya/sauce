---
title: Advent of Code 2024 - Day 3
date: 2024-12-03 16:00:00
description: RegExp day!
tags:
---
RegExp! Quick and fun one. I already think it can be shorter, but what the heck. I'll share my not so optimal solution anyway.

You can find [my implementation on GitHub](https://github.com/Gaya/aoc-2024/tree/main/src/03-mull-it-over) as always.

# Day 3 - Part One - RegExp

First thing we want to figure out is how to get the correct numbers from a string that looks kind of messy. `mul(123,123)` is what we need to look out for. A max of 3 numbers per argument.

I fired up [https://regex101.com/](https://regex101.com/) and put in the example string and got to writing the expression.

The first version of my RegExp looked like this:

```regexp
/mul\(([1-9][0-9]{0,2}),([1-9][0-9]{0,2})\)/gm
```

Look for anywhere in this string that start with `"mul("`, then capture a group with numbers ranging from 1 to 999. Then match on `","` and do the same capture for numbers again. Finally look for `")"` and continue for the rest of the input over multiple lines.

Got pointed out that you do not have to be as safe about the numbers as I was doing. The first number would never be `0`. So I updated it to:

```regexp
/mul\((\d{1,3}),(\d{1,3})\)/gm
```

With the matches neatly grouping the numbers I could go ahead and use them in TypeScript.

```typescript
const matches = input
  .matchAll(/mul\((\d{1,3}),(\d{1,3})\)/gm);

const numbers: [number, number][] = [];

for (let result of matches) {
  const [_, a, b] = result;
  numbers.push([
    parseInt(a, 10), 
    parseInt(b, 10),
  ]);
}

const ans = numbers.reduce((acc, [a, b]) => {
  return acc + (a * b);
}, 0);
```

I am first doing a `matchAll` to look for all the matches the RegExp will hit and then looping over those matches.

Each match holds the whole matched string as the first item of its array. The items that follow are the capture groups we define in the RegExp. So for us those would be the left and right number inside of `mul()`. We'll call these `a` and `b`.
We'll add parsed versions of those numbers into an array to use later, as pairs.

In the last few lines we'll loop over the number pairs we have and multiply those and add it to the total.

# Day 3 - Part Two - Enable/Disable

What I did here could have been a lot easier now that I think about it. I am going to do some extra RegExp searching to match `"don't()"` and `"do()"`. What I could have done is look for `don't()...do()` and remove all that is in between. But here we are. A less optimal solution, but a solution nonetheless.

```regexp
/mul\((\d{1,3}),(\d{1,3})\)|do(n't)?\(\)/gm
```

The RegExp stayed the same, but now adds a search for `do(n't)()`. `(n't)` is optional in this instance.

This means that not only `mul()` will be found, but also `don't()` and `do()`.

Now I used basically the same code as before, but with a slight update:

```typescript
let enabled = true;

for (let result of matches) {
  const [instruction, a, b] = result;
    
  if (instruction === 'do()') {
    enabled = true;
  } else if (instruction === 'don\'t()') {
    enabled = false;
  } else if (enabled || !withFilter) {
    numbers.push([
      parseInt(a, 10), 
      parseInt(b, 10),
    ]);
  }
}
```

`withFilter` is an argument I gave to the function to tell if it needs to perform the do / don't filter.

Any time it hits a `do()` or `don't()` it will enable or disable the adding of number to the total array. Because it's in an if/else block it will never go to the last clause if it's either of them.

The last clause check if the `mul()` is enabled, and if the filter is not enabled... just add the numbers anyway.

The rest of the process is basically the same.

All in all a nice puzzle and a great one to brush off a little bit of the rusty RegExp knowledge.

See you all tomorrow!
