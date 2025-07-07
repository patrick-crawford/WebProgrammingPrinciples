---
id: RegExp
title: RegExp
sidebar_position: 4
description: RegExp
---

# RegExp

A regular expression is a special string that describes a pattern to be used for matching or searching within other strings. They are also known as a _regex_ or _regexp_, and in JavaScript we refer to [`RegExp`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) when we mean the built-in `Object` type for creating and working with regular expressions.

You can think of regular expressions as a kind of mini programming language separate from JavaScript. They are not unique to JavaScript, and learning how to write and use them will be helpful in many other programming languages.

Even if you're not familiar with regular expression syntax (it takes some time to master), you've probably
encountered similar ideas with wildcards. Consider the following Unix command:

```bash
ls *.txt
```

Here we ask for a listing of all files whose filename _ends with_ the extension `.txt`. The `*` has a special meaning: _any character, and any number of characters_. Both `a.txt` and `file123.txt` would be matched against this pattern, since both end with `.txt`.

Regular expressions take the idea of defining patterns using characters like `*`, and extend it into a more powerful pattern matching language. Here's an example of a regular expression that could be used to match both common spellings of the word `"colour"` and `"color"`:

```js
colou?r
```

The `?` means that the preceding character `u` is optional (it may or may not be there).
Here's another example regular expression that could be used to match a string that starts with `id-` followed by 1, 2, or 3 digits (`id-1`, `id-12`, or `id-999`):

```js
id-\d{1,3}
```

The `\d` means a digit (0-9) and the `{1,3}` portion means _at least one, and at most three_. Together we get _at least one digit, and at most three digits_.

There are many [special characters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Using_special_characters) to learn with regular expressions, which we'll slowly introduce.

## Declaring JavaScript `RegExp`

Like `String` or `Array`, we can declare a `RegExp` using either a literal or the `RegExp` constructor:

```js
let regex = /colou?r/; // regex literal uses /.../
let regex2 = new RegExp('colou?r');
```

Regular expressions can also have [advanced search flags](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Advanced_searching_with_flags_2),
which indicate how the search is supposed to be performed.
These flags include `g` (globally match all occurrences vs. only matching once),
`i` (ignore case when matching), and `m` (match across line breaks, multi-line matching) among others.

```js
let regex = /pattern/gi; // find all matches (global) and ignore case
let regex2 = new RegExp('pattern', 'gi'); // same thing using the constructor instead
```

## Understanding Regular Expression Patterns

Regular expressions are dense, and often easier to write than to read. It's helpful to use
various tools to help you as you experiment with patterns, and try to understand and debug
your own regular expressions:

- [regexr.com](https://regexr.com/)
- [Regulex](https://jex.im/regulex)
- [regexpal.com](https://www.regexpal.com/)

### Matching Specific Characters

- `\ ^ $ . * + ? ( ) [ ] { } |` all have special meaning, and if you need to match them, you have to escape them with a leading `\`. For example: `\$` to match a `$`.

- Any other character will match itself. `abc` is a valid regular expression and means _match the letters abc_.

- The `.` means _any character_. For example `a.` would match `ab`, `a3`, or `a"`. If you need to match the `.` itself, make sure you escape it: `.\.` means _a period followed by any character_

- We specify a set of possible characters using `[]`. For example, if we wanted to match any vowel, we might do `[aeiou]`. This says _match any of the letters a, e, i, o, or u_ and would match `a` but not `t`. We can also do the opposite, and define a negated set: `[^aeiou]` would match anything that is _not_ a vowel. With regular expressions, it can often be easier to define your patterns in terms of what they are not instead of what they are, since so many things are valid vs. a limited set of things that are not. We can also specify a range, `[a-d]` would match any of `a, b, c, d` but not `f, g` or `h`.

- Some sets are so common that we have shorthand notation. Consider the set of single digit numbers, `[0123456789]`. We can instead use `\d` which means the same thing. The inverse is `\D` (capital `D`), and means `[^0123456789]` (i.e., _not one of the digits_). If we wanted to match a number with three digits, we could use `\d\d\d`, which would match `123` or `678` or `000`.

- Another commonly needed pattern is _any letter or number_ and is available with `\w`, meaning `[A-Za-z0-9_]` (all upper- and lower-case letters, digits 0 to 9, and the underscore). The inverse is available as `\W` and means `[^A-Za-z0-9_]` (everything _not_ in the set of letters, numbers and underscore).

- Often we need to match blank whitespace (spaces, tabs, newlines, etc.). We can do that with `\s`, and the inverse `\S` (anything not a whitespace). For example, suppose we wanted to allow users to enter an id number with or without a space: `\d\d\d\s?\d\d\d` would match both `123456` and `123 456`.

- There are lots of other examples of pre-defined common patterns, such as `\n` (newline), `\r` (carriage return), `\t` (tab). Consult the [MDN documentation for character classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp#Special_characters_meaning_in_regular_expressions) to lookup others.

### Define Character Matching Repetition

In addition to matching a single character or character class, we can also match sequences of them,
and define _how many_ times a pattern or match can/must occur. We do this by adding extra information
_after_ our match pattern.

- `?` is used to indicate that we want to match something _once or none_. For example, if we want to match the word `dog` without an `s`, but also to allow `dogs` (with an `s`), we can do `dogs?`. The `?` follows the pattern (i.e., `s`) that it modifies, and indicates that it is optional.

- `*` is used when we want to match _zero or more_ of something. `number \d*` would match `"number "` (no digits), `"number 1"` (one digit), and `"number 1234534123451334466600"`.

- `+` is similar to `*` but means _one or more_. `vroo+m` would match `"vroom"` but also `"vroooooooom"` and `"vroooooooooooooooooooooooooooooooom"`

- We can limit the number of matches to an exact number using `{n}`, which means _match exactly `n` times_. `vroo{3}m` would only match `"vroooom"`. We can further specify that we want a match to happen _match `n` or more times_ using `{n,}`, or use `{n,m}` to indicate we want to match \*at least `n` times and no more than `m` times: `\w{8,16}` would match 8 to 16 word characters, `"ABCD1234"` or `"zA5YncUI24T_3GHO"`

### Define Positional Match Parameters or Alternatives

Normally the patterns we define are used to look _anywhere_ within a string. However, sometimes
it's important to specify _where_ in the string a match is located. For example, we might care that
an id number _begins_ with some sequence of letters, or that a name doesn't _end_ with some set of characters.

- `^` means start looking for the match at the _beginning_ of the input string. We could test to see that a string begins with a capital letter like so: `^[A-Z]`.

- Similarly `$` means make sure that the match ends the string. If we wanted to test that string was a filename that ended with a period and a three letter extension, we could use: `\.\w{3}$` (an escaped period, followed by exactly 3 word characters, followed by the end of the string). This would match `"filename.txt"` but not `"filename.txt is a path"`.

- Sometimes we need to specify one of a number of possible alternatives. We do this with `|`, as in `red|green|blue` which would match any of the strings `"red"`, `"green"`, or `"blue"`.

## Using `RegExp` with `String`s

So far we've discussed how to declare a `RegExp`, and also some of the basics of defining search patterns.
Now we need to look at the different ways to use our regular expression objects to perform matches.

- [`RegExp.test(string)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) - used to test whether or not the given string matches the pattern described by the regular expression. If a match is made, returns `true`, otherwise `false`. `/id-\d\d\d/.test('id-123')` returns `true`, `/id-\d\d\d/.test('id-13b')` returns `false`.

- [`String.match(regexp)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) - used to find all matches of the given `RegExp` in the source `String`. These matches are returned as an `Array` of `String`s. For example, `'This sentence has 2 numbers in it, including the number 567'.match(/\d+/g)` will return the `Array` `['2', '567']` (notice the use of the `g` flag to find all matches globally).

- [`String.replace(regexp, replacement)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) - used to find all matches for the given `RegExp`, and returns a new `String` with those matches replaced by the replacement `String` provided. For example, `'50 , 60,75.'.replace(/\s*,\s*/g, ', ')` would return `'50, 60, 75.'` with all whitespace normalized around the commas.

- [`String.split(RegExp)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) - used to break the given `String` into an `Array` of sub-strings, dividing them on the `RegExp` pattern. For example, `'one-two--three---four----five-----six'.split(/-+/)` would return `['one', 'two', 'three', 'four', 'five', 'six']`, with elements split on any number of dashes.

There are other [methods you can call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Working_with_regular_expressions), and more [advanced ways to extract data](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions#Using_parentheses) using RegExp, and you are encouraged to dig deeper into these concepts over time. Thinking about matching in terms of regular expressions takes practice, and often involves inverting your logic to narrow a set of possibilities into something you can define in code.
