---
title: Advent of Code 2024 - Day 4
date: 2024-12-04 08:00:00
description: Word search in the form of a programming puzzle
tags:
---
Ah yes, a little word search inside a grid. Fun times ahead!

You can find [my implementation on GitHub](https://github.com/Gaya/aoc-2024/tree/main/src/04-ceres-search) as always.

# Day 4 - Part One - Finding XMAS

We need to find the word `XMAS` inside of a grid. It doesn't really matter which direction it's written. There can also be multiple hits in any direction.

My first thought was to turn our input into a usable grid. So split the lines and put the letters of each line in an array.

```typescript
const grid = input.split('\n')
  .map((line) => line.split(''));
```

So how do we find `XMAS` in this huge grid? I'd start by finding the first letter of `XMAS` in the grid. Let's write the base code for looping through the grid.

```typescript
for (let y = 0; y < grid.length; y++) {
  for (let x = 0; x < grid[y].length; x++) {
    // is grid[y][x] "X"?
  }
}
```

I knew that if we're going to look for letters on a grid we're going to start looking out of bounds soon. So I decided I wanted a simple function to retrieve a letter from the grid. If I request a position outside the grid: give back an empty string.

```typescript
function letterInGrid(
  grid: string[][], 
  y: number, 
  x: number,
): string {
  if (grid[y] && grid[y][x]) {
    return grid[y][x];
  }

  return '';
}
```

This means I can get letters from the grid using `lettersInGrid(grid, 0, 0)` etc.

We only need to start searching for `XMAS` if the letter we're at on the grid is `X`. We can skip searching on all other positions.

```typescript
for (let y = 0; y < grid.length; y++) {
  for (let x = 0; x < grid[y].length; x++) {
    if (letterInGrid(grid, y, x) === 'X') {
      // look for XMAS
    }
  }
}
```

Now... here is where I have to admit I am not really proud of my solution, but at least it works!

What I did was keep a list of directions to look in and whether we've on track to find `XMAS` or not.

This resulted in this ugly kind of state object to keep track of the state.

```typescript
const f = {
  e: true, s: true, w: true, n: true,
  ne: true, se: true, sw: true, nw: true,
}
```

A total of 8 possibilities for each wind direction to look in. Speaking of which... let's look at finding `XMAS` horizontally.

We'll loop over the remaining of the word `XMAS`, in this case `MAS` since we already found `X`. For each letter we're going to look one to the right in the grid.

```typescript
for (let w = 1; w < word.length; w++) {
  if (
    f.e 
    && word[w] !== letterInGrid(grid, y, x + w)
  ) {
    f.e = false;
  }
}
```

When the next letter in the word does not match the letter in the grid on the next position we mark `f.e` as failed. We do the same check for every wind direction. Yes. This is what I am not very proud of. Though this code skips checking if the wind direction failed earlier. So at least it's a bit optimised.

In the end we add up the wind directions which are still marked `true`.

```typescript
total += Object.values(f)
  .filter((v) => v).length;
```

`Object.values(f)` gives back an array of values which are assigned to the object's properties. In our case an array of booleans.

Check out the full loop of checking all eight wind directions [in the source on GitHub](https://github.com/Gaya/aoc-2024/blob/main/src/04-ceres-search/word-search.ts#L22-L54).

# Day 4 - Part Two - Finding crosses

This is actually a lot nicer. We need to find cases in the grid where `XMAS` crosses and it doesn't matter in which direction, but only diagonally. Actually... this part is easier!

First we look up the middle of the word: the letter `A`.

```typescript
for (let y = 0; y < grid.length; y++) {
  for (let x = 0; x < grid[y].length; x++) {
    if (letterInGrid(grid, y, x) === 'A') {
      // our code here
    }
  }
}
```

This means that we only need to check the letter to the top left, top right, bottom right, and bottom left.

After we got the letters we need to check if the top left is an `M` and bottom right is an `S`. Or the other way around. And the same for top right and bottom left.

```typescript
const nw = letterInGrid(grid, y - 1, x - 1);
const ne = letterInGrid(grid, y - 1, x + 1);
const se = letterInGrid(grid, y + 1, x + 1);
const sw = letterInGrid(grid, y + 1, x - 1);

const nwse = (nw === 'M' && se === 'S') 
  || (nw === 'S' && se === 'M');
const nesw = (ne === 'M' && sw === 'S') 
  || (ne === 'S' && sw === 'M');

if (nwse && nesw) {
  total++;
}
```

If both check succeed we can add one to the total.

# Conclusion

I am not really happy with how I check for `XMAS` in all wind directions and will probably see or think of a better solution later on. If I do and refactor it I will share it here.

See you tomorrow!
