---
id: Practice-Exercises
title: Practice Exercises
sidebar_position: 5
description: Practice Exercises
---

# Practice Exercises

1. Write a function `log` that takes an `Array` of `String`s and displays them on the `console`.

2. An application uses an `Array` as a Stack (LIFO) to keep track of items in a user's shopping history. Every time they browse to an item, you want to `addItemToHistory(item)`. How would you implement this?
3. Write a function `buildArray` that takes two `Number`s, and returns an `Array` filled with all numbers between the given number: `buildArray(5, 10)` should return `[5, 6, 7, 8, 9, 10]`
4. Write a function `addDollars` that takes an `Array` of `Number`s and uses the array's `map()` method to create and return a new `Array` with each element having a `$` added to the front: `addDollars([1, 2, 3, 4])` should return `['$1', '$2', '$3', '$4']`
5. Write a function `tidy` that takes an `Array` of `String`s and uses the array's `map()` method to create and return a new `Array` with each element having all leading/trailing whitespace removed: `tidy([' hello', ' world '])` should return `['hello', 'world']`.
6. Write a function `measure` which takes an `Array` of `String`s and uses the array's `forEach()` method to determine the size of each string in the array, returning the total: `measure(['a', 'bc'])` should return `3`. Bonus: try to rewrite your code using the `Array`'s [`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) method.
7. Write a function `whereIsWaldo` that takes an `Array` of `String`s and uses the array's `forEach()` method to create a new `Array` with only the elements that contain the text `"waldo"` or `"Waldo`" somewhere in them: `whereIsWaldo(['Jim Waldorf, 'Lynn Waldon', 'Frank Smith'])` should return `'Jim Waldorf, 'Lynn Waldon']`. Bonus: try to rewrite your code using the `Array`'s [`filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) method.
8. Write a function `checkAges` that takes two arguments: an `Array` of ages (`Number`); and a cut-off age (`Number`). Your function should return `true` if all of the ages in the `Array` are at least as old as the cut-off age: `checkAges([16, 18, 22, 32, 56], 19)` should return `false` and `checkAges([16, 18, 22, 32, 56], 6)` should return `true`. Bonus: try to rewrite your code using the `Array`'s [`every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) method.
9. Write a function `containsBadWord` that takes two arguments: `badWords` (an `Array` of words that can't be used), and `userName` (a `String` entered by the user). Check to see if any of the words in `badWords` are contained within `userName`. Return the `badWord` that was found, or `null` if none are found.
10. A `String` contains a Key/Value pair separated by a `":"`. Using `String` methods, how would you extract the two parts? Make sure you also deal with any extra spaces. For example, all of the following should be considered the same: `"colour: blue"`, `"colour:blue"`, `"colour : blue"`, `"colour: blue "`. Bonus: how could you use a `RegExp` instead?
11. A `String` named `addresses` contains a list of street addresses. Some of the addresses use short forms: `"St."` instead of `"Street"` and `"Rd"` instead of `"Road"`. Using `String` methods, convert all these short forms to their full versions.
12. Room booking codes must take the following form: room number (`1-305`) followed by `-` followed by the month as a number (`1-12`) followed by the day as a number (`1-31`). For example, all of the following are valid: `"1-1-1"`, `"250-10-3"`, `"66-12-12"`. Write a `RegExp` to check whether a room booking code is valid or not, which allows any of the valid forms.
13. Write a function that takes a `String` and checks whether or not it begins with one of `"Mr."`, `"Mrs."`, or `"Ms."`. Return `true` if it does, otherwise `false`. Bonus: try writing your solution using regular `String` methods _and_ again as a `RegExp`.
14. Write a function that takes a password `String`, and validates it according to the following rules: must be between 8-32 characters in length; must contain one Capital Letter; must contain one Number; must contain one Symbol (`!@#$%^&*-+{}`). Return `true` if the given password is valid, otherwise `false`.
15. Write a `RegExp` for a Canadian Postal Code, for example `"M3J 3M6"`. Allow spaces or no spaces, capitals or lower case.

## A Larger Problem Combining Everything:

You are [asked to write JavaScript code](files/exercise.js) to process a `String` which is in the form of a [Comma-Separated Values (CSV)](https://en.wikipedia.org/wiki/Comma-separated_values) formatted data dump of user information. The data might look something like this:

```csv
0134134,John Smith,555-567-2341,62 inches
0134135   ,    June    Lee    ,  5554126347 ,        149 cm
0134136,       Kim Thomas       , 5324126347, 138cm`
```

Write a series of functions to accomplish the following, building a larger program as you go. You can begin with [exercise.js](files/exercise.js):

1. Split the string into an `Array` of separate rows (i.e., an `Array` with rows separated by `\n`). Bonus: how could we deal with data that includes both Unix (`\n`) and Windows (`\r\n`) line endings?

2. Each row contains information user info: `ID`, `Name`, `Phone Number`, and `Height` info all separated by commas. Split each row into an `Array` with all of its different fields. You need to deal with extra and/or no whitespace between the commas.
3. Get rid of any extra spaces around the `Name` field
4. Using a `RegExp`, extract the Area Code from the `Phone Number` field. All `Phone Number`s are in one of two formats: `"555-555-5555"` or `"5555555555"`.
5. Check if the `Height` field has `"cm"` at the end. If it does, strip that out, convert the number to inches, and turn it into a `String` in the form `"xx inches"`. For example: `"152 cm"` should become `"59 inches"`.
6. After doing all of the above steps, create a new record with `ID`, `Name`, `Area Code`, `Height In Inches` and separate them with commas
7. Combine all these processed records into a new CSV formatted string, with rows separated by `\n`.

A sample solution is provided in [solution.js](files/solution.js).
