---
id: Practice-Exercises
title: Practice Exercises
sidebar_position: 3
description: Practice Exercises
---

# Practice Exercises

For each of the following, write a function that takes the given arguments, and returns
or produces (e.g., `console.log`) the given result.

1. Given `r` (radius) of a circle, calculate the area of a circle (A = π _ r _ r).

1. Simulate rolling a dice using `random()`. The function should allow the caller to specify any number of sides, but default to 6 if no side count is given: `roll()` (assume 6 sided, return random number between 1 and 6) vs. `roll(50)` (50 sided, return number between 1 and 50).
1. Write a function that converts values in Celcius to Farenheit: `convert(0)` should return `"32 F"`.
1. Modify your solution to the previous function to allow a second argument: `"F"` or `"C"`, and use that to determine what the scale of the value is, converting to the opposite: `convert(122, "F")` should return `"50 C"`.
1. Function taking any number of arguments (`Number`s), returning `true` if they are all less than 50: `isUnder50(1, 2, 3, 5, 4, 65)` should return `false`.
1. Function allowing any number of arguments (`Number`s), returning their sum: `sum(1, 2, 3)` should return `6`.
1. Function allowing any number of arguments of any type, returns `true` only if none of the arguments is falsy. `allExist(true, true, 1)` should return `true`, but `allExist(1, "1", 0)` should return `false`.
1. Function to create a JavaScript library name generator: `generateName("dog")` should return `"dog.js"`
1. Function to check if a number is a multiple of 3 (returns `true` or `false`)
1. Check if a number is between two other numbers, being inclusive if the final argument is true: `checkBetween(66, 1, 50, true)` should return `false`.
1. Function to calculate the HST (13%) on a purchase amount
1. Function to subtract a discount % from a total. If no % is given, return the original value.
1. Function that takes a number of seconds as a `Number`, returning a `String` formatted like `"X Days, Y Hours, Z Minutes"` rounded to the nearest minute.
1. Modify your solution above to only include units that make sense: `"1 Minute"` vs. `"3 Hours, 5 Minutes"` vs. `"1 Day, 1 Hour, 56 Minutes"` etc
1. Function that takes any number of arguments (`Number`s), and returns them in reverse order, concatenated together as a String: `flip(1, 2, 3)` should return `"321"`
1. Function that takes two `Number`s and returns their sum as an `Integer` value (i.e., no decimal portion): `intSum(1.6, 3.333333)` should return `4`
1. Function that returns the number of matches found for the first argument in the remaining arguments: `findMatches(66, 1, 345, 2334, 66, 67, 66)` should return `2`
1. Function to log all arguments larger than `255`: `showOutsideByteRange(1, 5, 233, 255, 256, 0)` should log `256` to the `console`
1. Function that takes a `String` and returns its value properly encoded for use in a URL. `prepareString("hello world")` should return `"hello%20world"`
1. Using the previous function, write an enclosing function that takes any number of `String` arguments and returns them in encoded form, concatenated together like so: `"?...&...&..."` where "..." are the encoded strings. `buildQueryString("hello world", "goodnight moon")` should return `"?hello%20world&goodnight%20moon"`
1. Function that takes a `Function` followed by any number of `Number`s, and applies the function to all the numbers, returning the total: `applyFn(function(x) { return x * x;}, 1, 2, 3)` should return 14.

After you try writing these yourself, take a look at a [possible solution](files/practice-exercises-solutions.js)
