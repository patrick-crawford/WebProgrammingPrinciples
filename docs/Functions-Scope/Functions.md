---
id: Functions
title: Functions
sidebar_position: 1
description: Functions
---

# Functions

A function is a _subprogram_, or a smaller portion of code that
can be called (i.e., invoked) by another part of your program, another function,
or by the environment in response to some user or device action (e.g., clicking a button,
a network request, the page closing). Functions _can_ take values (i.e., arguments)
and may _return_ a value.

Functions are first-class members of JavaScript, and play a critical role in developing
JavaScript programs. JavaScript functions can take other functions as arguments,
can return functions as values, can be bound to variables or `Object` properties, and
can even have their own properties. We'll talk about more of this when we visit JavaScript's
object-oriented features.

Learning to write code in terms of functions takes practice. JavaScript supports
[functional programming](https://en.wikipedia.org/wiki/Functional_programming). Web
applications are composed of lots of small components that need to get wired together
using functions, have to share data (i.e., state), and interoperate with other code
built into the browser, or in third-party frameworks, libraries, and components.

We use JavaScript functions in a number of ways. First, we encapsulate
a series of statements into higher-order logic, giving a name to a set of repeatable
steps we can call in different ways and places in our code. Second, we use them
to define actions to be performed in response to events, whether user initiated or
triggered by the browser. Third, we use them to define behaviours for objects, what
is normally called a _member function_ or _method_. Fourth, we use them to define
_constructor_ functions, which are used to create new objects. We'll look at all
of these in the coming weeks.

Before we dive into that, we'll try to teach you that writing many smaller functions
is often [better than having a few large ones](https://martinfowler.com/bliki/FunctionLength.html). Smaller code is [easier to test, easier to understand](https://dzone.com/articles/rule-30-%E2%80%93-when-method-class-or),
and generally [has fewer bugs](https://dubroy.com/blog/method-length-are-short-methods-actually-worse/).

## User-defined Functions

JavaScript has many built-in functions, which we'll get to below; however, it also
allows you to write your own and/or use functions written by other developers (libraries, frameworks).

These user-defined functions can take a number of forms.

### Function Declarations

The first is the _function declaration_, which looks like this:

```js
// The most basic function, a so-called NO OPERATION function
function noop() {}

// square function accepts one parameter `n`, returns its value squared.
function square(n) {
  return n * n;
}

// add function accepts two parameters, `a` and `b`, returns their sum.
function add(a, b) {
  return a + b;
}
```

Here the `function` keyword initiates a _function declaration_, followed by a
_name_, a _parameter list_ in round parenthesis, and the function's _body_ surrounded
by curly braces. There is no semi-colon after the function body.

### Function Expressions

The second way to create a function is using a _function expression_. Recall that
expressions evaluate to a value: a function expression evaluates to a `function` Object.
The resulting value is often bound (i.e., assigned) to a variable, or used as a parameter.

```js
let noop = function () {};

let square = function (n) {
  return n * n;
};

let add = function add(a, b) {
  return a + b;
};
```

A few things to note:

- The function's _name_ is often omitted. Instead we return an _anonymous function_ and bind it to a variable. We'll access it again via the variable name. In the case of recursive functions, we sometimes include it to make it easier for functions to call themselves. You'll see it done both ways.
- We _did_ use a semi-colon at the end of our function expression. We do this to signify the end of our assignment statement `let add = ... ;`.
- In general, _function declarations_ are likely a better choice (when you can choose) due to subtle errors introduced with declaration order and hosting (see below); however, both are used widely and are useful.

### Arrow Functions

Modern JavaScript also introduces a new function syntax called an [Arrow Function](https://eloquentjavascript.net/03_functions.html#h_/G0LSjQxoo) or "Fat Arrow". These functions are more terse, using the `=>` notation (not to be confused with the `<=` and `>=` comparison operators):

```js
let noop = () => {};

let square = (n) => n * n;

let add = (a, b) => a + b;
```

When you see `let add = (a, b) => a + b;` it is short-hand for `let add = function(a, b) { return a + b; }`, where `=>` replaces the `function` keyword and comes _after_ the parameter list, and the `return` keyword is optional, when functions return a single value.

Arrow functions also introduce some new semantics for the `this` keyword, which we'll address later.

You should be aware of Arrow functions, since many web developers use them heavily. However, don't feel pressure to use them yet if you find their syntax confusing.

### Parameters and `arguments`

Function definitions in both cases take parameter lists, which can be empty, single, or multiple
in length. Just as with variable declaration, no type information is given:

```js
function emptyParamList() {}

function singleParam(oneParameter) {}

function multipleParams(one, two, three, four) {}
```

A function can _accept_ any number of arguments when it is called, including none. This would
break in many other languages, but not JavaScript:

```js
function log(a) {
  console.log(a);
}

log('correct'); // logs "correct"
log('also', 'correct'); // logs "also"
log(); // logs undefined
```

Because we can invoke a function with any number of arguments, we have to write our functions
carefully, and test things before we make assumptions. How can we deal with a caller
sending 2 vs. 10 values to our function?

One way we do this is using the built-in [`arguments` Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments).

Every function has an implicit `arguments` variable available to it, which is an array-like
object containing all the arguments passed to the function. We can use `arguments.length` to obtain the actual number of arguments passed to the function at runtime, and use array index
notation (e.g., `arguments[0]`) to access an argument:

```js
function log(a) {
  console.log(arguments.length, a, arguments[0]);
}

log('correct'); // 1, "correct", "correct"
log('also', 'correct'); // 2, "also", "also"
log(); // 0, undefined, undefined
```

We can use a loop to access all arguments, no matter the number passed:

```js
function sum() {
  const count = arguments.length;
  let total = 0;
  for (let i = 0; i < count; i++) {
    total += arguments[i];
  }
  return total;
}

sum(1); // 1
sum(1, 2); // 3
sum(1, 2, 3, 4); // 10
```

You may have wondered previously how `console.log()` can work with one, two, three, or
more arguments. The answer is that all JavaScript functions work this way, and you can use it
to "overload" your functions with different argument patterns, making them useful
in more than one scenario.

### Parameters and `...`

Modern JavaScript also supports naming the "rest" of the parameters passed to a function. These [Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) allow us to specify that all final arguments to a function, no matter how many, should be available to the function as a named `Array`.

There are [some advantages](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters#Difference_between_rest_parameters_and_the_arguments_object) to _not_ using the implicit `arguments` keyword, which rest parameters provide.

We can convert the example above to this, naming our arbitrary list of "numbers":

```js
function sum(...numbers) {
  let total = 0;
  for (let i = 0; i < numbers.length; i++) {
    total += numbers[i];
  }
  return total;
}
```

### Dealing with Optional and Missing Arguments

Because we _can_ change the number of arguments we pass to a function at runtime, we
also have to deal with missing data, or optional parameters. Consider the case of
a function to calculate a player's score in a video game. In some cases we may want to
double a value, for example, as a bonus for doing some action a third time in a row:

```js
function updateScore(currentScore, value, bonus) {
  return bonus ? currentScore + value * bonus : currentScore + value;
}

updateScore(10, 3);
updateScore(10, 3);
updateScore(10, 3, 2);
```

Here we call `updateScore` three different times, sometimes with 2 arguments, and
once with 3. Our `updateScore` function has been written so it will work in both cases.
We've used a [conditional ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) to
decide whether or not to add an extra bonus score. When we say `bonus ? ... : ...` we are
checking to see if the `bonus` argument is _truthy_ or _falsy_--that is, did the caller provide a value for it? If they did, we do one thing, if not, we do another.

Here's another common way you'll see code like this written, using a default value:

```js
function updateScore(currentScore, value, bonus) {
  // See if `bonus` is truthy (has a value or is undefined) and use it, or default to 1
  bonus = bonus || 1;
  return currentScore + value * bonus;
}
```

In this case, before we use the value of `bonus`, we do an extra check to see if it
actually has a value or not. If it does, we use that value as is; but if it doesn't, we
instead assign it a value of `1`. Then, our calculation will always work, since multiplying
the value by `1` will be the same as not using a bonus.

The idiom `bonus = bonus || 1` is very common in JavaScript. It uses the
[Logical Or Operator `||`](<https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators#Logical_OR_()>) to test whether `bonus` evaluates to a value or not, and prefers that value if possible to the fallback default of `1`. We could also have written it out using an `if` statements like these:

```js
function updateScore(currentScore, value, bonus) {
  if (bonus) {
    return currentScore + value * bonus;
  }
  return currentScore + value;
}

function updateScore(currentScore, value, bonus) {
  if (!bonus) {
    bonus = 1;
  }
  return currentScore + value * bonus;
}
```

JavaScript programmers tend to use the `bonus = bonus || 1` pattern because it is
less repetitive, using less code, and therefore less likely to introduce bugs. We could
shorten it even further to this:

```js
function updateScore(currentScore, value, bonus) {
  return currentScore + value * (bonus || 1);
}
```

Because this pattern is so common, modern JavaScript has added a built-in way to handle [Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters). Instead of using `||` notation in the body of the function, we can specify a default value for any named parameter when it is declared. This frees us from having to check for, and set default values in the function body. Using default parameters, we could convert our code above to this:

```js
function updateScore(currentScore, value, bonus = 1) {
  return currentScore + value * bonus;
}
```

Now, if `bonus` has a value (i.e., is passed as a parameter), we use it; otherwise, we use `1` as a default.

### Return Value

Functions always _return_ a value, whether implicitly or explicitly. If the `return`
keyword is used, the expression following it is returned from the function. If
it is omitted, the function will return `undefined`:

```js
function implicitReturnUndefined() {
  // no return keyword, the function will return `undefined` anyway
}

function explicitReturnUndefined() {
  return;
  // return keyword, but no expression given, which is also `undefined`
}

function explicitReturn() {
  return 1;
  // return keyword, followed by `Number` expression evalutes to `Number`
}

function explicitReturn2() {
  return 'Hello' + ' World!';
  // return keyword, followed by expression evaluating to a `String`
}
```

### Function Naming

Functions are typically named using the same rules we learned for naming any
variable: `camelCase` and using the set of valid letters, numbers, etc. and avoiding
language keywords.

Function declarations always give a name to the function, while function expressions
often omit it, using a variable name instead:

```js
// Name goes after the `function` keyword in a declaration
function validateUser() {
    ...
}

// Name is used only at the level of the bound variable, function is anonymous
let validateUser = function() {
    ...
};

// Name is repeated, which is correct but not common. Used with recursive functions
let validateUser = function validateUser() {
    ...
};

// Names are different, which is also correct, but not common as it can lead to confusion
let validateUser = function validate() {
    // the validate name is only accessible here, within the function body
    ...
};
```

Because JavaScript allows us to bind function objects (i.e., result of function expressions)
to variables, it is common to create functions without names, but immediately pass them
to functions as arguments. The only way to use this function is via the argument name:

```js
// The parameter `fn` will be a function, and `n` a number
function execute(fn, n) {
  // Call the function referred to by the argument (i.e, variable) `fn`, passing `n` as its argument
  return fn(n);
}

// 1. Call the `execute` function, passing an anonymous function, which squares its argument, and the value 3
execute(function (n) {
  return n * n;
}, 3);

// 2. Same thing as above, but with different formatting
execute(function (n) {
  return n * n;
}, 3);

// 3. Same thing as above, using an Arrow Function
execute((n) => n * n, 3);

let doubleIt = function (num) {
  return num * 2;
};

// 4. Again call `execute`, but this time pass `doubleIt` as the function argument
execute(doubleIt, 3);
```

We can also use functions declared via function declarations used this way, and bind them to variables:

```js
function greeting(greeting, name) {
  return greeting + ' ' + name;
}

var sayHi = greeting; // also bind a reference to greeting to sayHi

// We can now call `greeting` either with `greeting()` or `sayHi()`
console.log(greeting('Hello', 'Steven'));
console.log(sayHi('Hi', 'Kim'));
```

JavaScript treats functions like other languages treat numbers or booleans, and lets
you use them as values. This is a very powerful feature, but can cause some confusion
as you get started with JavaScript.

You might ask why we would ever choose to define functions using variables. One common reason is to swap function implementations at runtime, depending on the state of the program. Consider the following code for displaying the user interface depending on whether the user is logged in or not:

```js
// Display partial UI for guests and non-authenticated users, hiding some features
function showUnauthenticatedUI() {
    ...
}

// Display full UI for authenticated users
function showAuthenticatedUI() {
    ...
}

// We will never call showUnauthenticatedUI or showAuthenticatedUI directly.
// Instead, we will use showUI to hold a reference to one or the other,
// and default to the unauthenticated version at first (i.e., until the user logs in).
let showUI = showUnauthenticatedUI;

...

// Later in the program, when a user logs in, we can swap the implementation
// without touching any of our UI code.
function authenticate(user) {
    ...
    showUI = showAuthenticatedUI;
}

...

// Whenever we need to refresh/display the UI, we can always safely call
// whichever function is currently bound to `showUI`.
showUI();
```

### Invoking Functions, the Execution Operator

In many of the examples above, we've been invoking (i.e., calling, running, executing) functions
but haven't said much about it. We invoke a function by using the `()` operator:

```js
let f = function () {
  console.log('f was invoked');
};
f();
```

In the code above, `f` is a variable that is assigned the value returned by a function expression. This means `f` is a regular variable, and we can use it like any other variable. For example, we could create another variable and share its value:

```js
let f = function () {
  console.log('f was invoked');
};
let f2 = f;
f(); // invokes the function
f2(); // also invokes the function
```

Both `f` and `f2` refer to the the same function object. What is the difference
between saying `f` vs. `f()` in the line `let f2 = f;`? When we write `f()`
we are really saying, "Get the value of `f` (the function referred to) and invoke it." However,
when we write `f` (without `()`), we are saying, "Get the value of `f` (the function referred to)" so that we can do something with it (assign it to another variable, pass it to a function, etc).

The same thing is true of function declarations, which also produce `function` Objects:

```js
function f() {
  console.log('f was invoked');
}
let f2 = f;
f2(); // also invokes the function
```

The distinction between referring to a function object via its bound variable name (`f`) vs
invoking that same function (`f()`) is important, because JavaScript programs treat functions
as _data_, just as you would a `Number`. Consider the following:

```js
function checkUserName(userName, customValidationFn) {
  // If `customValidationFn` exists, and is a function, use that to validate `userName`
  if (customValidationFn && typeof customValidationFn === 'function') {
    return customValidationFn(userName);
  }
  // Otherwise, use a default validation function
  return defaultValidationFn(userName);
}
```

Here the `checkUserName` function takes two arguments: the first a `String` for a username;
the second an optional (i.e., may not exist) function to use when validating this username.
Depending on whether or not we are passed a function for `customValidationFn`, we will either
use it, or use a default validation function (defined somewhere else).

Notice the line `if(customValidationFn && typeof customValidationFn === 'function') {` where
`customValidationFn` is used like any other variable (accessing the value it refers to vs. doing an invocation), to check if it has a value, and if its value is actually a function. Only then is it save to invoke it.

It's important to remember that JavaScript functions aren't executed until they are called
via the invocation operator, and may also be used as values without being called.

## Built-in/Global Functions

JavaScript provides a small number of [built-in global functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects#Function_properties) for working with its data types, for example:

- [`parseInt()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)
- [`parseFloat()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)
- [`isNaN()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN)
- [`isFinite()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isFinite)
- [`decodeURI()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI)
- [`decodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURIComponent)
- [`encodeURI()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI)
- [`encodeURIComponent()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent)

There are also global functions that exist for historical reasons, but should be avoided for performance, usability, and/or security reasons:

- [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) dangerous to parse and run user-defined strings
- [`prompt()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/prompt) and [`alert()`](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) synchronous calls that block the UI thread.

Most of JavaScripts "standard library" comes in the form of _methods_ on global objects
vs. global functions. A _method_ is a function that is bound to a variable belonging
to an object, also known as a _property_. We'll be covering these in more depth later, but
here are some examples

- [`console.*`](https://developer.mozilla.org/en-US/docs/Web/API/console). There are
  quite a few worth learning, but here are some to get you started:
  _ [`console.log()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/log), [`console.warn()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/warn), and [`console.error()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/error)
  _ [`console.assert()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/assert)
  _ [`console.count()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/count)
  _ [`console.dir()`](https://developer.mozilla.org/en-US/docs/Web/API/Console/dir)
- [`Math.*`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)
  - [`Math.abs()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/abs)
  - [`Math.max()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/max)
  - [`Math.min()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/min)
  - [`Math.random()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random)
  - [`Math.round()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/round)
- [`Date.*`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)
  - [`Date.now()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now)
  - [`Date.getTime()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTime)
  - [`Date.getMonth()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getMonth)
  - [`Date.getDay()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getDay)
- [`JSON.*`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)
  - [`JSON.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)
  - [`JSON.stringify()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

Much of web programming is done using `Objects` and calling their methods. JavaScript is a small language, but the ecosystem of `Objects`, APIs, libraries, and frameworks allows it to do anything.

## Suggested Readings

- [ExploringJS, Chapter 15. Functions](http://exploringjs.com/es5/ch15.html) and [Chapter 16. Variables: Scopes, Environments, and Closures](http://exploringjs.com/es5/ch16.html)
- [Eloquent JavaScript, Chapter 3. Functions](https://eloquentjavascript.net/03_functions.html)
- [Functions Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions) and [Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions) on MDN.
