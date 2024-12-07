---
title: Advent of Code 2024 - Day 7
date: 2024-12-07 05:00:00
description: A great example of thinking outside of the exponential box
tags:
---
A few days went by without any posts. Both days I didn't feel like I pulled some cool tricks. Though I did try to solve day 5 with just RegExp, it was kind of slow. This day however kind of made me think in recursion, but we actually do not really need it!

You can find [my implementation on GitHub](https://github.com/Gaya/aoc-2024/tree/main/src/07-bridge-repair) as always.

# Day 7 - Parsing of reasoning

This day's puzzle is quite interesting. On paper, it looks pretty easy, but to program this without brute forcing of recursion could be a difficult task.

In a nutshell the task is to find if an outcome is possible if you place the `+` or `*` operator in an equation and test for all possible equations. Oh, and we go from left to right, so no need to take math notation and order into account.

We get the following equation:

```
3267: 81 40 27
```

And basically have to turn it into the following:

```
3267 === 81 + 40 + 27
3267 === 81 * 40 + 27
3267 === 81 * 40 * 27
3267 === 81 + 40 * 27
```

If one of these passes. It is correct.

The amount of equations to test grows exponentially so we need to be wary of that!

For my parser I wanted to turn the input into `number[][]` where the first number is the number before `:` and the other numbers would be the numbers in the equation on the right side of `:`.

```typescript
export function parseInput(
  input: string,
): number[][] {
  return input.split('\n')
    .map((line) => line
      .replace(':', '')
      .split(' ')
      .map((n) => parseInt(n, 10)));
}
```

I split the input into rows. Each row I replace the `:` with an empty string and then split on `' '` and parsing the strings into numbers. Not that special.

So now that we have a list of equations... how are we going to turn a single equation in 4 different tests?

# Day 7 - Recursion?

My first plan was to loop over all the numbers in the equation, calculate all the possible outcomes, and then see if the number we are checking for is in that list of outcomes.

```typescript
const outcomes = numbers
  .reduce((acc: number[], num, index) => {
    if (index === 0) {
      return [num];
    }
  
    return acc
      .reduce((newAcc: number[], lastNum) => {
        return [
          ...newAcc,
          lastNum + num,
          lastNum * num,
        ];
      }, []);
}, []);
```

This one made my head spin for sure! Had a lot of other solutions, but this one is the easiest to explain.

`numbers` are the numbers we need to build our equations with. I start with a `reduce` on those numbers and give an empty array as my starting point.

Each iteration will return the last calculations of the numbers as far as we've seen. Let's take `[81, 40, 27]` with this piece of code.

First iteration: `acc = [], num = 81, index = 0`

We have nothing to calculate with yet, thus I'll return the number to calculate with (first number of the list) back wrapped in an array.

Second iteration: `acc = [81], num = 40, index = 1`

Now we can add some outcomes to the array. So for each number in `acc` we are going to add a calculation for `+` and `*`. This means we both get `81 + 40` and `81 * 40` back.

Third iteration: `acc = [121, 3240], num = 27, index = 2`

Now we will do the same with the numbers in `acc`, this time resulting in a lot more outcomes. `121 + 27`, `121 * 27`, `3240 + 27`, `3240 * 27`.

The result of these outcomes is: `[148, 3267, 3267, 87480]`. Then we can check if `3267` is in here and tell our program that this equation is possible!

# Day 7 - Small optimisations

In the puzzle input we will work with much greater numbers and amount of number in equations. So it's best to ignore equation paths which are not possible anyway.

This code pushes values into the possibilities only if they do not exceed the `outcome` we are looking for. I know it's not best practise to manipulate the argument of a function, but in this case it's quite safe as it's an empty array I created before. 

```typescript
const outcomes = numbers
  .reduce((acc: number[], num, index) => {
    if (index === 0) {
      return [num];
    }
  
    return acc
      .reduce((newAcc: number[], lastNum) => {
        const added = lastNum + num;
        if (added <= outcome) {
          newAcc.push(added);
        }

        const product = lastNum * num;
        if (product <= outcome) {
          newAcc.push(product);
        }
        
        return newAcc;
      }, []);
}, []);
```

This will skip a lot of calculations we do not have to do.

# Day 7 - Part 2

Parts two was a bit easier, and I knew I couldn't just put numbers together as strings, but rather have to be a bit smarter about it.

The added new rule is that number in an equation can we stuck together. For instance: `81 + 40` and `81 * 40` can now also be `8140`.

Some notes: `outcome` is the outcome we test for. `withConcat` is to tell to support concatenation of numbers as an operator.

```typescript
function len(input: number): number {
  return Math.floor(Math.log10(input)) + 1;
}

const outLength = len(outcome);

const outcomes = numbers
  .reduce((acc: number[], num, index) => {
    if (index === 0) {
      return [num];
    }
  
    return acc
      .reduce((newAcc: number[], lastNum) => {
        const added = lastNum + num;
        if (added <= outcome) {
          newAcc.push(added);
        }

        const product = lastNum * num;
        if (product <= outcome) {
          newAcc.push(product);
        }

        if (withConcat) {
          const numLength = len(num);

          if (
            len(lastNum) + numLength 
            <= outLength
          ) {
            newAcc.push(
              (
                lastNum 
                * Math.pow(10, numLength)
              ) + num
            );
          }
        }
        
        return newAcc;
      }, []);
}, []);
```

First I had to look up for I can determine the length of a number, counting the digits. I didn't want to convert to string, which I could have, but I looked up a mathematical solution to the problem. Apparently it's a pretty simple calculation:

```typescript
Math.floor(Math.log10(1234)) + 1 // 4
```

I use that to determine the lengths of outcome, previous equation outcome, and the number to calculate with. If the lengths of the previous outcome and number to add are longer than the whole of the outcome, then it will never work so we can skip it.

In order to create a new combined number I use a simple trick. Take for instance the numbers `12` and `345`. If you want to make `12345` you'd write a sum like: `12000 + 345`. Our goal is to get `12` to `12000`. Which is achieved by doing `12 * 1000`. And how do we know how to make `1000` based on `345`? That is `10 ** 3` where 3 is the length of the number `345`.

That was a long train of thought, but translated into a line of code it would be:

```typescript
(12 * Math.pow(10, 3) + 1) + 345
```

# Conclusion

I thought it was a fun puzzle where my mind first drifted into recursion and endless loops, but eventually was quite flat and not so recursive in the end.

Looking forward to the other puzzles!
