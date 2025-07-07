---
id: Introduction-JavaScript
title: Introduction to JavaScript
sidebar_position: 3
description: Introduction to JavaScript
---

# Introduction to JavaScript

The first front-end web technology we will learn is JavaScript. JavaScript (often shortened to JS)
is a lightweight, interpreted or JIT (i.e., Just In Time) compiled language meant to be
embedded in host environments, for example, web browsers.

JavaScript looks [similar to C/C++ or Java](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Introduction#JavaScript_and_the_ECMAScript_Specification#JavaScript_and_Java) in some of its syntax, but is quite different
in philosophy; it is more closely related to [Scheme](<https://en.wikipedia.org/wiki/Scheme_(programming_language)>) than C. For example, JavaScript is a dynamic scripting language supporting
multiple programming styles, from [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming) to [imperative](https://en.wikipedia.org/wiki/Imperative_programming) to [functional](https://en.wikipedia.org/wiki/Functional_programming).

JavaScript is one of, if not the [most popular programming languages in the world](https://redmonk.com/sogrady/2023/05/16/language-rankings-1-23/), and has been for many years.
Learning JavaScript well will be a tremendous asset to any software developer, since so
much of the software we use is built using JS.

> JavaScript's many versions: JavaScript is an evolving language, and you'll hear it [referred to by a number of names](https://medium.freecodecamp.org/whats-the-difference-between-javascript-and-ecmascript-cba48c73a2b5), including: ECMAScript (or ES), ES5, ES6, ES2015, ES2017, ..., ES2021, ES2022, etc. [ECMA is the European Computer Manufacturers Association, which is the standards body responsible for the JS language](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Introduction#JavaScript_and_the_ECMAScript_Specification). As the standard evolves, the specification goes through different versions, adding or changing features and syntax. In this course we will primarily focus on ECMAScript 6 (ES6) and newer versions, which all browsers support. We will also sometimes use new features of the language, which most browsers support. Language feature support across browsers is [maintained in this table](http://kangax.github.io/compat-table/es2016plus/).

## JavaScript Resources

Throughout the coming weeks, we'll make use of a number of important online resources.
They are listed here so you can make yourself aware of them, and begin to explore on your own.
All programmers, no matter how experienced, have to return to these documents on
a routine basis, so it's good to know about them.

- [JavaScript on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
  - [JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
  - [JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
- [Eloquent JavaScript](https://eloquentjavascript.net/)
- [JavaScript for impatient programmers (ES2022 edition)](https://exploringjs.com/impatient-js/index.html)

## JavaScript Environments

Unlike C, which is compiled to machine code, JavaScript is meant to be run within a host
environment. There are many possible environments, but we will focus on the following:

- Web Browsers, and their associated developer tools, primarily:
  - [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools/)
  - [Firefox Developer Tools](https://developer.mozilla.org/en-US/docs/Tools)
- [node.js](https://nodejs.org/), and its [command line REPL (Read-Eval-Print-Loop)](http://www.tutorialsteacher.com/nodejs/nodejs-console-repl)

If you haven't done so already, you should install all of the above.

### JavaScript Engines

JavaScript is parsed, executed, and managed (i.e., memory, garbage collection, etc) by an [engine](https://en.wikipedia.org/wiki/JavaScript_engine) written in C/C++.
There are a number of JavaScript engines available, the most common of which are:

- [V8](https://developers.google.com/v8/), maintained an used by Google in Chrome and in node.js
- [SpiderMonkey](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey), maintained and used by Mozilla in Firefox
- [ChakraCore](https://github.com/microsoft/chakracore), maintained and used by Microsoft in Edge
- [JavaScriptCore](https://trac.webkit.org/wiki/JavaScriptCore), maintained and used by Apple in Safari

These engines, much like car engines, are meant to be used within a larger context. We will
encounter them indirectly via web browsers and in node.js.

It's not important to understand a lot about each of these engines at this point,
other than to be aware that each has its own implementation of the ECMAScript standards, its own performance characteristics (i.e., some are faster at certain things), as well as its own set of bugs.

### Running JavaScript Programs

JavaScript statements can be stored in an external file with a `.js` file extension,
or embedded within HTML code via the HTML `<script>` element. As a developer, you also
have a number of options for writing and executing JavaScript statements or files:

1. From the command line via [node.js](https://nodejs.org/en/). You'll learn more about node.js in subsequent courses, but we'll also use it sometimes in this course to quickly try test JavaScript expressions, and to run JavaScript programs outside the browser.

2. Using [Firefox's Developer Tools](https://developer.mozilla.org/en-US/docs/Tools), and in particular the [Web Console](https://developer.mozilla.org/en-US/docs/Tools/Web_Console), [JavaScript Debugger](https://developer.mozilla.org/en-US/docs/Tools/Debugger), and [Scratchpad](https://developer.mozilla.org/en-US/docs/Tools/Scratchpad).

3. Using [Chrome's DevTools](https://developers.google.com/web/tools/chrome-devtools/), and in particular the [Console](https://developers.google.com/web/tools/chrome-devtools/console/get-started) and [Sources Debugger](https://developers.google.com/web/tools/chrome-devtools/javascript/)

4. Finally, we'll eventually write JavaScript that connects with HTML and CSS to create dynamic web pages and applications.

Take some time to install and familiarize yourself with all of the methods listed above.

## JavaScript Syntax

### Recommend Readings

We will spend a month learning JavaScript, and there is no one best way to do it.
The more you read and experiment the better. The following chapters/pages give a good overview:

- [Chapter 1. Basic JavaScript](http://exploringjs.com/es5/ch01.html) of [Exploring JS (ES5)](http://exploringjs.com/es5).
- [MDN JavaScript Introduction Tutorial](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)
- [Chapter 1. Values, Types and Operators](https://eloquentjavascript.net/2nd_edition/01_values.html) and [Chapter 2. Program Structure](https://eloquentjavascript.net/2nd_edition/02_program_structure.html) of [Eloquent JavaScript (2nd Ed.)](https://eloquentjavascript.net/2nd_edition/).

#### Important Ideas

- Like C, JavaScript is Case-Sensitive: `customerCount` is not the same thing as `CustomerCount` or `customercount`
- Name things using `camelCase` (first letter lowercase, subsequent words start with uppercase) vs. `snake_case`.
- Semicolons are optional in JavaScript, but highly recommended. We'll expect you to use them in this course, and using them will make working in C++, Java, CSS, etc. much easier, since you have to use them there.

- Comments work like C/C++, and can be single or multi-line

```js
// This is a single line comment. NOTE: the space between the // and first letter.

/*
 This is a multi-line comment,
 and can be as long as you need.
 */
```

- Whitespace: JavaScript will mostly ignore whitespace (spaces, tabs, newlines). In this course we will expect you to use good indentation practices, and for your code to be clean and readable. Many web programmers use [Prettier](https://prettier.io/) to automatically format their code, and we will too:

```js
// This is poorly indented, and needs more whitespace
function add(a, b) {
  if (!b) {
    return a;
  } else {
    return a + b;
  }
}

// This is much more readable due to the use of whitespace
function add(a, b) {
  if (!b) {
    return a;
  } else {
    return a + b;
  }
}
```

- JavaScript statements: a JavaScript program typically consists of a series of statements. A statement is a single-line of instruction made up of objects, expressions, variables, and events/event handlers.
- Block statement: a block statement, or compound statement, is a group of statements that are treated as a single entity and are grouped within curly brackets `{...}`. Opening and closing braces need to work in pairs. For example, if you use the left brace `{` to indicate the start of a block, then you must use the right brace `}` to end it. The same matching pairs applies to single `'......'` and double `"......."` quotes to designate text strings.

- [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions) are one of the primary building blocks of JavaScript. A function defines a subprogram that can be called by other parts of your code. JavaScript treats functions like other built-in types, and they can be stored in variables passed to functions, returned from functions or generated at run-time. Learning how to write code in terms of functions will be one of your primary goals as you get used to JavaScript.

- Variables are declared using the [`let` keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let). You must use the `let` keyword to precede a variable name, but you do not need to provide a type, since the initial value will set the type.

> JavaScript version note: JavaScript also supports the [`var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var) and [`const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) keywords for variable declaration. We will primarily use `let` in this course, but be aware of `var` and `const` as well, which other developers will use.

```js
let year;
let seasonName = 'Fall';

// Referring to and using syntax:
year = 2023;
console.log(seasonName, year);
```

- JavaScript Variables: variables must start with a letter (`a-zA-z`), underscore (`_`), or dollar sign (`$`). They cannot be a [reserved (key) word](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords). Subsequent characters can be letters, numbers, underscores.

_NOTE_: If you forget to use the `let` keyword, JavaScript will still allow you to use a variable, and simply create a _global variable_. We often refer to this as "leaking a global," and it should always be avoided:

```js
let a = 6; // GOOD: a is declared with let
b = 7; // BAD: b is used without declaration, and is now a global
```

- Data Types: JavaScript is a typeless language--you don't need to specify a type for your data (it will be inferred at runtime). However, internally, the [following data types are used](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Overview):
  - [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Numbers) - a double-precision 64-bit floating point number. Using `Number` you can work with both Integers and Floats. There are also some special `Number` types, [`Infinity`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity) and [`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN).
  - [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt) - a value that can be too large to be represented by a `Number` (larger than [`Number. MAX_SAFE_INTEGER`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER),) can be represented by a `BigInt`. This can easily be done by appending `n` to the end of an integer value.
  - [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Strings) - a sequence of Unicode characters. JavaScript supports both single (`'...'`) and double (`"..."`) quotes when defining a `String`.
  - `Boolean` - a value of `true` or `false`. We'll also see how JavaScript supports so-called _truthy_ and _falsy_ values that are not pure `Boolean`s.
  - `Object`, which includes [`Function`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript#Functions), [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array), [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date), and many more. - JavaScript supports object-oriented programming, and uses objects and functions as first-class members of the language.
  - [`Symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol) - a primitive type in JavaScript that represents a unique and anonymous value/identifier. They can normally be used as an object's unique properties.
  - [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null) - a value that means "this is intentionally nothing" vs. `undefined`
  - [`undefined`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined) - a special value that indicates a value has never been defined.

| Declaration                   | Type        | Value                                 |
| ----------------------------- | ----------- | ------------------------------------- |
| `let s1 = "some text";`       | `String`    | `"some text"`                         |
| `let s2 = 'some text';`       | `String`    | `"some text"`                         |
| `let s3 = '172';`             | `String`    | `"172"`                               |
| `let s4 = '172' + 4;`         | `String`    | `"1724"` (concatenation vs. addition) |
| `let n1 = 172;`               | `Number`    | `172` (integer)                       |
| `let n2 = 172.45;`            | `Number`    | `172.45` (double-precision float)     |
| `let n3 = 9007199254740993n;` | `BigInt`    | `9007199254740993n` (integer)         |
| `let b1 = true;`              | `Boolean`   | `true`                                |
| `let b2 = false;`             | `Boolean`   | `false`                               |
| `let b3 = !b2;`               | `Boolean`   | `true`                                |
| `let s = Symbol("Sym");`      | `symbol`    | `Symbol(Sym)`                         |
| `let c;`                      | `undefined` | `undefined`                           |
| `let d = null;`               | `object`    | `null`                                |

Consider a simple program from your C course, and how it would look in JavaScript

```c
 // Area of a Circle, based on https://scs.senecac.on.ca/~btp100/pages/content/input.html
 // area.c

 #include <stdio.h>               // for printf

 int main(void)
 {
    const float pi = 3.14159f;   // pi is a constant float
    float radius = 4.2;          // radius is a float
    float area;                  // area is a float

    area = pi * radius * radius; // calculate area from radius

    printf("Area = %f\n", area); // copy area to standard output

    return 0;
}
```

Now the same program in JavaScript:

```js
const pi = 3.14159; // pi is a Number
let radius = 4.2; // radius is a Number
let area; // area is (currently) undefined

area = pi * radius * radius; // calculate area from radius

console.log('Area = ' + area); // print area to the console
```

We could also have written it like this, using [`Math.PI`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/PI), which we'll learn about later:

```js
let radius = 4.2; // radius is a Number
let area = Math.PI * radius * radius; // calculate area from radius

console.log('Area', area); // print area to the console
```

- Common [JavaScript Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators) (there are more, but these are a good start):

| Operator                  | Operation                      | Example                                                                          |
| ------------------------- | ------------------------------ | -------------------------------------------------------------------------------- |
| `+`                       | Addition of `Number`s          | `3 + 4`                                                                          |
| `+`                       | Concatenation of `String`s     | `"Hello " + "World"`                                                             |
| `-`                       | Subtraction of `Number`s       | `x - y`                                                                          |
| `*`                       | Multiplication of `Number`s    | `3 * n`                                                                          |
| `/`                       | Division of `Number`s          | `2 / 4`                                                                          |
| `%`                       | Modulo                         | `7 % 3` (gives 1 remainder)                                                      |
| `++`                      | Post/Pre Increment             | `x++`, `++x`                                                                     |
| `--`                      | Post/Pre Decrement             | `x--`, `--x`                                                                     |
| `=`                       | Assignment                     | `a = 6`                                                                          |
| `+=`                      | Assignment with addition       | `a += 7` same as `a = a + 7`. Can be used to join `String`s too                  |
| `-=`                      | Assignment with subtraction    | `a -= 7` same as `a = a - 7`                                                     |
| `*=`                      | Assignment with multiplication | `a *= 7` same as `a = a * 7`                                                     |
| `/=`                      | Assignment with division       | `a /= 7` same as `a = a / 7`                                                     |
| `&&`                      | Logical `AND`                  | `if(x > 3 && x < 10)` both must be `true`                                        |
| `()`                      | Call/Create                    | `()` invokes a function, `f()` means invoke/call function stored in variable `f` |
| <code>&#124;&#124;</code> | Logical `OR`                   | <code>if(x === 3 &#124;&#124; x === 10)</code> only one must be `true`           |
| <code>&#124;</code>       | Bitwise `OR`                   | <code>3.1345&#124;0</code> gives `3` as an integer                               |
| `!`                       | Logical `NOT`                  | `if(!(x === 2))` negates an expression                                           |
| `==`                      | Equal                          | `1 == 1` but also `1 == "1"` due to type coercion                                |
| `===`                     | Strict Equal                   | `1 === 1` but `1 === "1"` is not `true` due to types. Prefer `===`               |
| `!=`                      | Not Equal                      | `1 != 2`, with type coercion                                                     |
| `!==`                     | Strict Not Equal               | `1 !== "1"`. Prefer `!==`                                                        |
| `>`                       | Greater Than                   | `7 > 3`                                                                          |
| `>=`                      | Greater Than Or Equal          | `7 >=7` and `7 >= 3`                                                             |
| `<`                       | Less Than                      | `3 < 10`                                                                         |
| `<=`                      | Less Than Or Equal             | `3 < 10` and `3 <=3`                                                             |
| `typeof`                  | Type Of                        | `typeof "Hello"` gives `'string'`, `typeof 6` gives `'number'`                   |
| `cond ? a : b`            | Ternary                        | `status = (age >= 18) ? 'adult' : 'minor';`                                      |

> JavaScript version note: you may encounter `=>` in JavaScript code, which looks very similar to `<=` or `>=`. If you see `=>` it is an [arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions), which is new ES6 syntax for declaring a function expression. We will slowly introduce this syntax, especially in later courses.

- JavaScript is dynamic, and variables can change value _and_ type at runtime:

```js
let a; // undefined
a = 6; // 6, Number
a++; // 7, Number
a--; // 6, Number
a += 3; // 9, Number
a = 'Value=' + a; // "Value=9", String
a = !!a; // true, Boolean
a = null; // null
```

- JavaScript is a [garbage collected language](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Memory_Management). Unlike C, memory automatically gets freed at runtime when variables are not longer in scope or reachable. We still need to be careful not to leak memory (i.e., hold onto data longer than necessary, or forever) and block the garbage collector from doing its job.

- Strings: JavaScript doesn't distinguish between a single `char` and a multi-character `String`--everything is a `String`. You [define a `String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) using either single (`'...'`), double (`"..."`) quotes. Try to pick one style and stick with it within a given file/program vs. mixing them.

- JavaScript version note: newer versions of ECMAScript also allow for the use of [template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals). Instead of `'` or `"`, a template literal uses \` (backticks), and you can also [interpolate expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Expression_interpolation).

- A JavaScript [expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Expressions) is any code (e.g., literals, variables, operators, and expressions) that evaluates to a single value. The value may be a `Number`, `String`, an `Object`, or a logical value.

```js
let a = 10 / 2; // arithmetic expression
let b = !(10 / 2); // logical expression evaluates to false
let c = '10 ' + '/' + ' 2'; // string, evaluates to "10 / 2"
let f = function () {
  return 10 / 2;
}; // function expression, f can now be called via the () operator
let d = f(); // f() evaluates to 10/2, or the Number 5
```

- JavaScript execution flow is determined using the following four (4) basic control structures:
  - Sequential: an instruction is executed when the previous one is finished.
  - Conditional: a logical condition is used to [determine which instruction will be executed next](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/conditionals) - similar to the `if` and `switch` statements in C (which JavaScript also has).
  - Looping: a series of [instructions are repeatedly executed](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Looping_code) until some condition is satisfied - similar to the `for` and `while` statements in C (which JavaScript also has). There are many different types of loops in JavaScript: for example [`for` loops](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Looping_code#The_standard_for_loop) and [`while` loops](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Looping_code#while_and_do_..._while), as well as ways to [`break`](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Looping_code#Exiting_loops_with_break) out of loops or skip iterations with [`continue`](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Looping_code#Skipping_iterations_with_continue). We'll cover other types as we learn about `Object` and `Array`.
  - Transfer: [jump to, or invoke](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions) a different part of the code - similar to calling a function in C.

```js
/**
 * 1. Sequence example: each statement is executed one after the other
 **/
let a = 3;
let b = 6;
let c = a + b;

/**
 * 2. Conditional examples: a decision is made based on the evaluation of an expression,
 * and a code path (or branch) taken.
 **/
let grade;
let mark = 86;

if (mark >= 90) {
  grade = 'A+';
} else if (mark >= 80) {
  grade = 'A';
} else if (mark >= 70) {
  grade = 'B';
} else if (mark >= 60) {
  grade = 'C';
} else if (mark >= 50) {
  grade = 'D';
} else {
  grade = 'F';
}

switch (grade) {
  case 'A+':
    // do these steps if grade is A+
    break;
  case 'A':
    // do these steps if grade is A
    break;
  case 'B':
    // do these steps if grade is B
    break;
  case 'C':
    // do these steps if grade is C
    break;
  case 'D':
    // do these steps if grade is D
    break;
  default:
    // do these steps in any other case
    break;
}

/**
 * 3. Looping example: a set of statements are repeated
 **/

let total = 0;
for (let i = 1; i < 11; i++) {
  total += i;
  console.log('i', i, 'total', total);
}

/**
 * 4. Transfer example: a set of statements are repeated
 **/

function add(a, b) {
  // declaring the add function
  if (!b) {
    // check if the b argument exists/has a value
    return a; // if not, simply return the value of argument a
  }
  return a + b; // otherwise, return the two arguments added together
}

let total;
total = add(56); // invoking the add function with a single argument
total = add(total, 92); // invoking the add function with two arguments
```
