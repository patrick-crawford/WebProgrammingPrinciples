---
id: Strings
title: Strings
sidebar_position: 2
description: Strings
---

# Strings

Here are a few examples of how you can declare a [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) in JavaScript, first using a string literal, followed by a call to the [`new` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new) and the `String` object's constructor function:

```js
/*
 * JavaScript String Literals
 */
let s = 'some text'; // single-quotes
let s1 = 'some text'; // double-quotes
let s2 = `some text`; // template literal using back-ticks
let unicode =
  '中文 español Deutsch English देवनागरी العربية português বাংলা русский 日本語 ਪੰਜਾਬੀ 한국어 தமிழ் עברית'; // non-ASCII characters

/*
 * JavaScript String Constructor: `new String()` creates a new instance of a String
 */
let s3 = new String('Some Text');
let s4 = new String('Some Text');
```

If we want to convert other types to a `String`, we have a few options:

```js
let x = 17;
let s = '' + x; // concatenate with a string (the empty string)
let s2 = String(x); // convert to String. Note: the `new` operator is not used here
let s3 = x.toString(); // use a type's .toString() method
```

Whether you use a literal or the constructor function, in all cases you will be able to use
the various [functionality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/prototype#Properties) of the [`String` type](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String).

## String Properties and Methods

- [`s.length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length) - will tell us the length of the string (UTF-16 code units)
- [`s.charAt(1)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charAt) - returns the character at the given position (UTF-16 code unit). We can also use `s[1]` and use an index notation to get a particular character from the string.
- [`s.concat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/concat) - returns a new string created by concatenating the original with the given arguments.
- [`s.padStart(2, '0)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padStart) - returns a new string padded with the given substring until the length meets the minimum length given. See also [`s.padEnd()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/padEnd).
- [`s.includes("tex")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes) - returns `true` if the search string is found within the string, otherwise `false` if not found.
- [`s.startsWith("some")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith) - returns `true` if the string starts with the given substring, otherwise `false`.
- [`s.endsWith("text")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith) - returns `true` if the string ends with the given substring, otherwise `false`.
- [`s.indexOf("t")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/indexOf) - returns the first index position of the given substring within `s`, or `-1` if the substring is not found within `s`. See also [`s.lastIndexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/lastIndexOf)
- [`s.match(regex)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) - tries to match a regular expression against the string, returning the matches. See discussion of RegExp below.
- [`s.replace(regex, "replacement")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) - returns a new string with the first occurrence of a matched RegExp replaced by the replacement text. See also [`s.replaceAll()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replaceAll), which replaces _all_ occurrences.
- [`s.slice(2, 3)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) - returns a new string extracted (sliced) from within the original string. A beginning index and (optional) end index mark the position of the slice.
- [`s.split()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) - returns an Array (see discussion below) of substrings by splitting the original string based on the given separator (`String` or `RegExp`).
- [`s.toLowerCase()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toLowerCase) - returns a new string with all characters converted to lower case.
- [`s.toUpperCase()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) - returns a new string with all characters converted to upper case.
- [`s.trim()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim) - returns a new string with leading and trailing whitespace removed.

> JavaScript Version Note: modern JavaScript also supports [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals), also sometimes called template _strings_. Template literals use back-ticks instead of single- or double-quotes, and allow you to interpolate JavaScript expressions. For example:

```js
let a = 1;
let s = 'The value is ' + 1 * 6;
// Use ${...} to interpolate the value of an expression into a string
let templateVersion = `The value is ${1 * 6}`;
```
