---
id: Practice-Exercises
title: Practice Exercises
sidebar_position: 4
description: Practice Exercises
---

# Practice Exercises

Try to solve each of the following using JavaScript. If you need to `print` something,
use `console.log()`, which will print the argument(s) you give it.

1. Create a variable `label` and assign it the value `"senecacollege"`. Create another variable `tld` and assign it `"ca"`. Create a third variable `domainName` that combines `label` and `tld` to produce the value `"senecacollege.ca"`.

1. Create a variable `isSeneca` and assign it a boolean value (`true` or `false`) depending on whether or not `domainName` is equal to `"senecacollege.ca"`. HINT: use `===` and don't write `true` or `false` directly.
1. Create a variable `isNotSeneca` and assign it the inverse boolean value of `isSeneca`. HINT: if `isSeneca` is `true`, `isNotSeneca` should be `false`.
1. Create four variables `byte1`, `byte2`, `byte3`, `byte4`, and assign each of these a value in the range `0-255`.
1. Convert `byte1` to a `String` using `.toString()`, and `console.log()` the result. What happens if you use `toString(2)` or `toString(16)` instead?
1. Create a variable `ipAddress` and assign it the value of combining your four `byteN` variables together, separated by `"."`. For example: `"192.168.2.1"`.
1. Create a variable `ipInt` and assign it the integer value of bit-shifting (`<<`) and adding your `byteN` variables. HINT: your `ipInt` will contain 32 bits, the first byte needs to be shifted 24 bit positions (`<< 24`) so it occupies 32-25, the second shifted 16, the third 8.
1. Create a variable `ipBinary` that contains the binary representation of the `ipInt` value. HINT: use `.toString(2)` to display the number with `1` and `0` only.
1. Create a variable `statusCode`, and assign it the value for the "I'm a teapot" HTTP status code. HINT: see [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
1. Write an `If` statement that checks to see if your `statusCode` is a [`4xx` client error](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#Client_error_responses). HINT: use the `<`, `>`, `>=`, and/or `<=` operators to test the value
1. Write a `switch` statement that checks your `statusCode` for all possible [`1xx` information responses](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#Information_responses). In each case, you should `console.log()` the response text associated with the status code, or `"unknown information response"` if the status code is not known.
1. Write a function `is2xx(status)` which takes a status code `status` (e.g., `200`) and returns `true` if the status code is a [valid 2xx code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#Successful_responses).
1. Create a variable `studentName` and assign your name. Create another variable `studentAge` and assign it your age. Use `console.log()` to print out a sentence that includes both variables, like `"Alice is 20 years old."`.
1. Create a variable `isEven` and assign it a boolean value (`true` or `false`) depending on whether a given number `num` is even or not. HINT: use the modulus operator `%`.
1. Create a variable `isOdd` and assign it the inverse boolean value of `isEven`. HINT: if `isEven` is `true`, `isOdd` should be `false`.
1. Create a variable `radius` and assign it a value of `10`. Calculate the area of a circle with this radius and assign the result to a variable `area`. HINT: use `Math.PI` and the formula `area = πr^2`.
1. Create a variable `temperatureInCelsius` and assign it a value. Convert this temperature to Fahrenheit and assign the result to a variable `temperatureInFahrenheit`. HINT: use the formula `F = C * 9/5 + 32`.
1. Create a variable `heightInFeet` and assign it a value. Convert this height to meters and assign the result to a variable `heightInMeters`. HINT: use the conversion factor `1 foot = 0.3048 meters`.
1. Create a variable `seconds` and assign it a value. Convert this time to minutes and seconds (e.g., 90 seconds becomes 1 minute and 30 seconds) and assign the result to two variables `minutes` and `remainingSeconds`.
1. Create a variable `score` and assign it a value. Write an `if` statement that checks if the score is an A (90-100), B (80-89), C (70-79), D (60-69), or F (below 60) and assigns the result to a variable `grade`.
1. Write a `switch` statement that checks the value of a variable `day` and `console.log()`s whether it is a weekday or weekend. HINT: `day` can be a value from 1 (Monday) to 7 (Sunday).
1. Write a function `isPositive(num)` which takes a number `num` and returns `true` if the number is positive and `false` otherwise.
1. Write a function `isLeapYear(year)` which takes a year `year` and returns `true` if the year is a leap year and `false` otherwise. HINT: a leap year is divisible by 4, but not by 100, unless it is also divisible by 400.
1. Write a function `getDayOfWeek(day)` which takes a number `day` (from 1 to 7) and returns the day of the week as a string (e.g., "Monday").
1. Write a function `getFullName(firstName, lastName)` which takes two strings `firstName` and `lastName` and returns the full name as a single string.
1. Write a function `getCircleArea(radius)` which takes a number `radius` and returns the area of a circle with that radius.
1. Write a function `getHypotenuse(a, b)` which takes two numbers `a` and `b` (the lengths of the two sides of a right triangle) and returns the length of the hypotenuse. HINT: use the Pythagorean theorem and `Math.sqrt()` to calculate the square root.

After you try writing these yourself, take a look at a [possible solution](files/practice-exercises-solution.js).
