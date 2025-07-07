---
id: Scope-Closures
title: Scope & Closures
sidebar_position: 2
description: Scope & Closures
---

# Scope

JavaScript variables were historically _declared_ with the `var` keyword. Modern JavaScript has switched to `let`, `const`. The way each works is different, and it's important to understand these differences.

We often _assign_ a value when we _declare_ it, though we don't have to do both at once:

```js
let x; // declared, no assignment (value is `undefined`)
x = 7; // assignment of previously declared variable
let y = x; // declaration and assignment combined
```

A variable always has a _scope_, which is the location(s) in the code where it
is usable. Consider the variables `total` and `value`, as well as the
`add` function below:

```js
var total = 7; // global variable, accessible everywhere

function add(n) {
  var value = total + n; // local variable, accessible anywhere within the function only
  return value;
}

console.log('Total is', total); // Works, because `total` is in the same scope
console.log('Value is', value); // `undefined`, since `value` isn't defined in this scope
console.log('New Total', add(16)); // Works, because `add` is defined in the same scope
```

When using the `var` keyword, variables use _function scope_, while variables declared with `let` and `const` use _block scope_. Coming from C/C++, using `let` and `const` will likely feel more familiar`:

```c
int main()
{
  {
      int x = 10;       // x is declared with block scope
  }
  {
      printf("%d", x);  // Error: x is not accessible here
  }
  return 0;
}
```

Now in JavaScript:

```js
function main() {
  {
    var x = 10; // x is declared in a block, but is scoped to `main`
  }
  {
    console.log(x); // works, because `x` is accessible everywhere in `main`
  }
}
```

Because variables declared using `var` have **function scope**, programmers tended to define them at the top of their functions. They don't strictly need to do this, since JavaScript will _hoist_ or raise all variables declared with `var` in a function to the top of the function's scope:

```js
function f() {
  var y = x + 1;
  var x = 2;
}
```

At runtime, this will be transformed into the following:

```js
function f() {
    var x;          // declaration is hoisted (but not assignment) to the top

    var y = x + 1;  // `NaN`, since `undefined` + 1 can't be resolved
    x = 2;          // note: `x` is not declared above, only the assignment is now here
```

This also happens when we forget to declare a local variable:

```js
function f() {
  x = 2; // `x` is assigned a value, but not declared
  return x + 1;
}
```

At runtime, this will be transformed into the following:

```js
var x; // `x` is not found in the scope of `f`, so it becomes global

function f() {
  x = 2;
  return x + 1;
}
```

The previous example introduces another important concept with JavaScript scopes, namely,
that scopes can be _nested_ within one another. Hoisting is moving variable declarations to the beginning of a scope. For example, function declarations are hoisted completely, which means we can call a function _before_ we declare it.

```js
f(); // this will work, as f's declaration gets hoisted
function f() {}
f(); // this will also work, because f has been declared as you expect.

g(); // this will not work, since g's declaration will be hoisted, but not the assignment.
var g = function () {};
```

Many of the confusing aspects of function scope and hoisting are solved by using `let` and `const`, which work at the block level instead. Consider these two loops:

```js
// Version 1 using var
for (var i = 0; i < 10; i++) {
  console.log('The value of i is ' + i);
}

// Version 2 using let
for (let i = 0; i < 10; i++) {
  console.log('The value of i is ' + i);
}
```

In the preceding code, the scope of `i` is different in version 1 vs. 2. In version 1, the declaration of `i` will actually cause a variable to be created in the scope of the owning function. This may or may not be what you expect (i.e., the variable `i` will exist outside the loop). In version 2, this is not the case, and `i` is scoped to the function body only (i.e., you can't access it before or after the loop).

We're discussing both function and block scopes because JavaScript supports each of them, and code you'll work on will use both methods. It's important to understand each approach.

For new code that you write, you are encouraged to prefer `let` and `const` and use block scope.

## Overwriting Variables in Child Scopes

Since variables defined with `var` have function scope, and because functions can be nested, we have to be careful when naming our variables and arguments so as to not overwrite a variable in a parent scope. Or, we can use this to temporarily do exactly that. In both cases, we need to understand how nested scopes work.

Consider the the following code, where a variable named `x` is used in three different scopes. What will be printed to the `console` when `child` is called?

```js
var x = 1;

function parent() {
  var x = 2;

  function child(x) {
    console.log(x);
  }

  child(3);
}
```

The first declaration of `x` creates a global variable (i.e., available in every scope).
Then, in `parent` we re-declare `x`, creating a new local variable, which overwrites (or hides)
the global variable `x` in this scope (i.e., within the body of `parent`). Next, we define
yet another scope for `child`, which also uses `x` as the name of its only argument (essentially
another local variable). When we do `child(3)`, we are binding the value `3` to the `x`
argument defined for the scope of `child`, and in so doing yet again overwriting the parent `x`.
In the end, the console will show `3`.

We can do this in error as well, and cause unexpected behaviour:

```js
var total = 5;

function increase(n) {
  var total = n + n;
}

increase(50);
console.log(total);
```

Here we expect to see `100` but instead will get `5` on the `console.` The problem is
that we have redefined, and thus overwritten `total` inside the `increase` function. During
the call to `increase`, the new local variable `total` will be used, and then go out of scope.
After the function completes, the original global variable `total` will again be used.

## Closures

A closure is a function that has _closed over_ a scope, retaining this scope even after it would
otherwise disappear through the normal rules of execution. In the following function, the
variable `x` goes out of scope as soon as the function finishes executing:

```js
function f() {
  var x = 7;
  return x * 2;
  // After this return, and f completes, `x` will no longer be available.
}
```

In JavaScript, functions have access not only to their own local variables, but also
to any variables in their parents' scope. That is, if a variable is used (referenced)
but not declared in a function, JavaScript will visit the parent scope to find the variable.
This can happen for any number of child/parent levels up to the global level.

The following is an example of this, and probably one you've seen before:

```js
var x = 7;

function f() {
  return x * 2; // `x` not declared here, JS will look in the parent scope (global)
}
```

Consider this example:

```js
function parent() {
  var x = 7;

  function child() {
    return x * 2;
  }

  return child();
}
```

Here `x` is used in `child`, but declared in `parent`. The `child` function has access
to all variables in its own scope, plus those in the `parent` scope. This nesting of scopes
relies on JavaScript's function scope rules, and allows us to share data.

Sometimes we need to capture data in a parent scope, and retain it for a longer period of time
than would otherwise be granted for a given invocation. Consider this example:

```js
function createAccumulator(value) {
  return function (n) {
    value += n;
    return value;
  };
}

var add = createAccumulator(10);
add(1); // returns 11
add(2); // returns 13
```

Here the `createAccumulator` function takes an argument `value`, the initial value to use
for an accumulator function. It returns an anonymous function which takes a value `n` (a `Number`) and adds it to the `value` before returning it. The `add` function is created by invoking `createAccumulator` with the initial `value` of `10`. The function that is returned by `createAccumulator` has access to `value` in its parent's scope. Normally, `value` would be
destroyed as soon as `createAccumulator` finished executing. However, we have created a _closure_ to capture the variable `value` in a scope that is now attached to the function we're creating and returning. As long as the returned function exists (i.e., as long as `add` holds on to it), the variable `value` will continue to exist in our child function's scope: the variables that existed when this function was created continue to live on like a memory, attached to the lifetime of the returned function.

Closures make it possible to _associate_ some _data_ (i.e., the environment) with a
function that can then operate on that data. We see similar strategies in pure
object-oriented languages, where data (properties) can be associated with an object,
and functions (methods) can then operate on that data. Closures play a somewhat
similar role, however, they are more lightweight and allow for dynamic (i.e., runtime)
associations.

By connecting data and functionality, closures help to reduce global variables, provide
ways to "hide" data, allow a mechanism for creating private "methods", avoid overwriting
other variables in unexpected ways.

As we go further with JavaScript and web programming, we will encounter many instances
where closures can be used to manage variable lifetimes, and associated functions with
specific objects. For now, be aware of their existence, and know that it is an advanced
concept that will take some time to fully master. This is only our first exposure to it.

Another way we'll see closures used, is in conjunction with [Immediately-Invoked Function Expressions (IIFE)](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression). Consider
the following rewrite of the code above:

```js
let add = (function (value) {
  return function (n) {
    value += n;
    return value;
  };
})(10);

add(1); // returns 11
add(2); // returns 13
```

Here we've declared `add` to be the value of invoking the anonymous function expression
written between the first `(...)` parentheses. In essence, we have created a function
that gets executed immediately, and which returns another function that we will use
going forward in our program.

This is an advanced technique to be aware of at this point, but not one you need to master
right away. We'll see it used, and use it ourselves, in later weeks to to avoid global variables, simulate block scope in JavaScript, and to choose or generate function implementations at runtime (e.g., [polyfill](https://remysharp.com/2010/10/08/what-is-a-polyfill)).
