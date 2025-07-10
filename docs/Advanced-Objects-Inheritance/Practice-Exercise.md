---
id: Practice-Exercise
title: Practice Exercise
sidebar_position: 3
description: Practice Exercise
---

# Practice Exercise

## Morse Code translator

[Morse code](https://en.wikipedia.org/wiki/Morse_code) is a system of encoding developed
in the 1800s that allowed transmission of textual messages over signal systems that only
supported on/off (1 and 0) notations.

Complete the program below as specified. Your program should be able to translate messages like
`-- --- .-. ... ./-.-. --- -.. .` into `MORSE CODE` and vice versa. Use what you learned
above about `Object`s, and also some of the built-in `Object`s we've studied, in particular
`RegExp` and `String`.

Use the following [limited set of morse code](https://morsecode.scphillips.com/morse2.html) to use in this exercise. You could expand your program to handle more complex messages later if you want:

| Letter  | Morse  |
| ------- | ------ |
| A       | `.-`   |
| B       | `-...` |
| C       | `-.-.` |
| D       | `-..`  |
| E       | `.`    |
| F       | `..-.` |
| G       | `--.`  |
| H       | `....` |
| I       | `..`   |
| J       | `.---` |
| K       | `-.-`  |
| L       | `.-..` |
| M       | `--`   |
| N       | `-.`   |
| O       | `---`  |
| P       | `.--.` |
| Q       | `--.-` |
| R       | `.-.`  |
| S       | `...`  |
| T       | `-`    |
| U       | `..-`  |
| V       | `...-` |
| W       | `.--`  |
| X       | `-..-` |
| Y       | `-.--` |
| Z       | `--..` |
| _space_ | `/`    |

NOTE: letters are separated by a single space (`' '`) within a word, and words are separated with a `/`.
For example, the words `MORSE CODE` would translate to `-- --- .-. ... ./-.-. --- -.. .`

```js
// Object to provide lookup of morse code (value) for a given letter (key).
let alpha = {
  // define the mapping here as a literal
};

// Object to provide lookup of letter (value) for a given morse code (key).
let morse = {};
// Hint: use the [] operator to specify these special key values rather than a literal.

// Return `true` if all characters are morse code.  Use a RegExp.
function isMorse(characters) {}

// Return `true` if all characters are part of the alphabet defined in `alpha`.  Use a RegExp.
// Bonus: can you rewrite it using `Object.keys()` and your `alpha` Object instead?
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
function isAlpha(characters) {}

// Given an alphabet message, convert and return in morse code.  Use your morse and/or alpha object.
// Return undefined if text is not alpha.
function textToMorse(text) {}

// Given a morse code message, convert and return in text.  Use your morse and/or alpha object.
// Return undefined if morse is not proper code.
function morseToText(morse) {}

// Message class that takes a `message` (String), which can be either morse or alpha.
// Use your functions above to decide how to store a value for `any` on `this`
class Message {
  constructor(text) {}

  // Return the message as morse code, converting if necessary
  toMorse() {}

  // Return the message as alpha characters, converting if necessary
  toAlpha() {}
}

let msg1 = new Message(
  '--- -... .--- . -.-. - .../.. -./.--- .- ...- .- ... -.-. .-. .. .--. -/.- .-. ./...- . .-. -.--/.--. --- .-- . .-. ..-. ..- .-..'
);
console.log(msg1.toAlpha());
console.log(msg1.toMorse());

let msg2 = new Message('I am learning how to use Objects in JavaScript');
console.log(msg2.toMorse());
console.log(msg2.toAlpha());
```

You can download the [code above](files/example.js) as well as a [possible solution](files/solution.js).
