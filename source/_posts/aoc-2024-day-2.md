---
title: Advent of Code 2024 - Day 2
date: 2024-12-03 13:00:00
description: Dissecting day two of Advent of Code day 2 in TypeScript
tags:
---
The solution for this day got some post completion refactors in order to improve the readability and make code a bit quicker.

You can find [my implementation on GitHub](https://github.com/Gaya/aoc-2024/tree/main/src/02-red-nosed-reports) as always.

# Day 2 - Part One - Parsing

The first thing we want to do is look at the puzzle input and turn it into usable variables we can work with in our code. We are going to check an array of numbers against the rules set by the puzzle.

The example shows the following input string:

```
7 6 4 2 1
1 2 7 8 9
9 7 6 2 1
1 3 2 4 5
8 6 4 4 1
1 3 6 7 9
```

And we want to turn it into a workable structure like:

```typescript
const reports = [
  [7, 6, 4, 2, 1],
  [1, 2, 7, 8, 9],
  [9, 7, 6, 2, 1],
  [1, 3, 2, 4, 5],
  [8, 6, 4, 4, 1],
  [1, 3, 6, 7, 9],
];
```

I actually don't think we need regexp here and just use the built-in JavaScript string methods to chop up the string in a workable structure.

```typescript
const reports = input
    .split('\n')
    .map((line) => {
      return line.split(' ')
        .map((i) => parseInt(i, 10))
    });
```

First we split the lines of numbers into multiple strings by splitting on `\n` essentially turning the input into the following:

```typescript
const reports = [
  '7 6 4 2 1',
  '1 2 7 8 9',
  '9 7 6 2 1',
  '1 3 2 4 5',
  '8 6 4 4 1',
  '1 3 6 7 9',
];
```

Then, from line 3 of the implementation, you see we're mapping over all the items we found. In this we're going to split on `" "` and then map `parseInt` on all those split strings, so we have a nice list of numbers.

# Day 2 - Part One - Is the report safe?

There are a couple of this we need to check from a report to see if it is safe. First question: is the distance between the current number and the one before more than 0 and 3 or less. Those are the easiest to check.

```typescript
return numbers.every((current, i) => {
  if (i === 0) {
    return true;
  }
  
  const prev = numbers[i - 1];
  const distance = current - prev;
    
  if (
    distance === 0
    || Math.abs(distance) > 3
  ) {
    return false;
  }

  return true;
});
```

You'll that I use `number.every`, this means that every single one of the callbacks has to succeed. It's going to start with the first item in the array (called `current` in this code) and run the code inside to check if the report is safe or not.

The first number in the report is always safe as there is nothing to compare to, so we give it an okay immediately.

Then we're grabbing the previous number by getting the `i - 1` from the same array, meaning the number for the current.

The distance (negative or positive) is calculated by subtracting the current from the previous. The great thing here is that we also know the direction the distance is going, so is it going up or down. Positive means up, negative means down. We need to keep that in mind for the next set of rules.

Finally, we check if the distance is 0 or if the distance is larger than 3. If it is one of these, return `false`.

Next we need to check if the direction is only going up or down. And fail if not.

```typescript
return numbers.every((current, i) => {
  if (i === 0) {
    return true;
  }
  
  const prev = numbers[i - 1];
  const distance = current - prev;
  const prevPrev = numbers[i - 2];
  const direction = prevPrev !== undefined 
    ? prev - prevPrev : 0;
    
  if (
    distance === 0
    || Math.abs(distance) > 3
    || (direction < 0 && distance > 0)
    || (direction > 0 && distance < 0)
  ) {
    return false;
  }

  return true;
});
```

In order to check if what direction we're going we need to get the number before the previous and compare those two against each other like we did with the distance.
If there is no "previous previous" number, we can assume there is no direction, and thus we need not check.

If the result of the subtraction is positive, the direction of the two previous numbers is up, and if negative, it's down.

Then we add the check we need to do in the if statement for it. If direction is up and now we're going down: fail. And also the other way around.

Great. That's part one sorted.

# Day 2 - Part Two - Dampening

Aha! Now we need to perform the same safety check, but we need to remove a number from the report and see if any will succeed. This actually kind of nicely hooks into what I've already written.

For each check that fails and has dampening enabled I am going to generate a list of reports with just one number missing of the same report we're working on. So a report of 5 numbers would result in 5 new reports. Let's generate those new reports to check:

```typescript
const reports = numbers
  .map((_, j) => numbers
    .filter((_, index) => index !== j));
```

For each number in the current report we generate a new report of number, but without the current we're generating by filtering on the index.

These new reports have to be checked too. So with the new `reports` we can use `.some` to check if any of those new reports would work. Just like so:

```typescript
const dampenedSafe = reports
  .some((report) => isSafe(report));
```

In the end we can combine all we've learned into the following:

```typescript
export function isSafe(
  numbers: number[], 
  dampener = false,
): boolean {
  return numbers.every((current, i) => {
    if (i === 0) {
      return true;
    }

    const prev = numbers[i - 1];
    const distance = current - prev;
    const prevPrev = numbers[i - 2];
    const direction = prevPrev !== undefined
      ? prev - prevPrev : 0;

    if (
      distance === 0
      || Math.abs(distance) > 3
      || (direction < 0 && distance > 0)
      || (direction > 0 && distance < 0)
    ) {
      if (dampener) {
        return numbers
          .map((_, j) => numbers
            .filter((_, index) => index !== j))
          .some((report) => isSafe(report));
      }

      return false;
    }

    return true;
  });
}
```

That was a fun quick one! I just finished day 3, so I better start writing about it too.
