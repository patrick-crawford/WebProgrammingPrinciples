---
id: Arrays
title: Arrays
sidebar_position: 3
description: Arrays
---

# Arrays

An [`Array`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) is an `Object` with various [properties and methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Array_instances) we can use for working with lists in JavaScript.

## Declaring JavaScript Arrays

Like creating a `String`, we can create an `Array` in JavaScript using either a literal or the `Array` constructor function:

```js
let arr = new Array(1, 2, 3); // array constructor
let arr2 = [1, 2, 3]; // array literal
```

Like arrays in C, a JavaScript `Array` has a length, and items contained within it can be
accessed via an index:

```js
let arr = [1, 2, 3];
let len = arr.length; // len is 3
let item0 = arr[0]; // item0 is 1
```

Unlike languages such as C, a JavaScript `Array` can contain any type of data, including mixed types:

```js
let list = [0, '1', 'two', true];
```

JavaScript `Array`s can also contain holes (i.e., be missing certain elements), change size dynamically at runtime, and we don't need to specify an initial size:

```js
let arr = []; // empty array
arr[5] = 56; // element 5 now contains 56, and arr's length is now 6
```

> NOTE: a JavaScript `Array` is really a **map**, which is a data structure that associates values with unique keys (often called a key-value pair). JavaScript arrays are a special kind of map that uses numbers for the keys, which makes them look and behave very much like arrays in other languages. We will encounter this **map** structure again when we look at how to create `Object`s.

## Accessing Elements in an Array

Like arrays in C, we can use index notation to obtain an element at a given index:

```js
let numbers = [50, 12, 135];
let firstNumber = numbers[0];
let lastNumber = numbers[numbers.length - 1];
```

JavaScript also allows us to use a technique called [Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to unpack values in an Array (or Object, see below) into distinct variables. Consider each of the following methods, both of which accomplish the same goal:

```js
// Co-ordinates for Seneca's Newnham Campus
let position = [43.796, -79.3486];

// Separate the two values into their own unique variables.

// Version 1 - index notation
let lat = position[0];
let lng = position[1];

// Version 2 - destructure
let [lat, lng] = position;
```

This technique is useful when working with structured data, where you know exactly how many elements are in an array, and need to access them:

```js
let dateString = `17/02/2001`;
let [day, month, year] = dateString.split('/');
console.log(`The day is ${day}, month is ${month}, and year is ${year}`);
```

Here we `.split()` the string `'17/02/2001'` at the `'/'` character, which will produce the Array `['17', '02', '2001']`. Next, we destructure this Array's values into the variables `day`, `month`, `year`.

You can also ignore values (i.e., only unpack the one or ones you want):

```js
let dateString = `17/02/2001`;
// Ignore the first index in the array, unpack only position 1 and 2
let [, month, year] = dateString.split('/');
console.log(`The month is ${month}, and year is ${year}`);

let emailAddress = `jsmith@myseneca.ca`;
// Only unpack the first position, ignoring the second
let [username] = emailAddress.split('@');
console.log(`The username for ${emailAddress} is ${username}`);
```

## `Array` Properties and Methods

- [`arr.length`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/length) - a property that tells us the number of elements in the array.

### Methods that modify the original array

- [`arr.push(element)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) - a method to add one (or more) element(s) to the end of the array. Using `push()` modifies the array (increasing its size). You can also use [`arr.unshift(element)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift) to add one (or more) element to the _start_ of the array.
- [`arr.pop()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop) - a method to remove the last element in the array and return it. Using `pop()` modifies the array (reducing its size). You can also use [`arr.shift()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift) to remove the _first_ element in the array and return it.

### Methods that do not modify the original array

- [`arr.concat([4, 5], 6)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat) - returns a new array with the original array joined together with other arrays or values provided.
- [`arr.includes(element)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) - returns `true` if the array includes the given element, otherwise `false`.
- [`arr.indexOf(element)`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf) - returns the index of the given element in the array, if it exists, otherwise `-1` (meaning not found).
- [`arr.join("\n")`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join) - returns a string created by joining (concatenating) all elements in the array with the given delimiter (`String`).

### Methods for iterating across the elements in an Array

JavaScript's `Array` type also provides a [long list](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#) of useful methods for working with list data. All of
these methods work in roughly the same way:

```js
// Define an Array
let list = [1, 2, 3, 4];

// Define a function that you want to call on each element of the array
function operation(element) {
  // do something with element...
}

// Call the Array method that you want, passing your function operation
list.arrayOperation(operation);
```

JavaScript will call the given function on every element in the array, one after
the other. Using these methods, we are able to work with the elements in an Array
instead of only being able to do things with the Array itself.

As a simple example, let's copy our `list` Array and add 3 to every element.
We'll do it once with a for-loop, and the second time with the `forEach()` method:

```js
// Create a new Array that adds 3 to every item in list, using a for-loop
let listCopy = [];

for (let i = 0; i < list.length; i++) {
  let element = list[i];
  element += 3;
  listCopy.push(element);
}
```

Now the same code using the `Array`'s `forEach()` method:

```js
let listCopy = [];

list.forEach(function (element) {
  listCopy.push(element + 3);
});
```

We've been able to get rid of all the indexing code, and with it, the chance
for [off-by-one errors](https://en.wikipedia.org/wiki/Off-by-one_error). We
also don't have to write code to get the element out of the list: we just use
the variable passed to our function.

These `Array` methods are so powerful that there are often functions that do
exactly what we need. For example, we could shorten our code above even further
but using the `map()` method. The `map()` method takes one `Array`, and calls
a function on every element, creating and returning a new `Array` with those
elements:

```js
let listCopy = list.map(function (element) {
  return element + 3;
});
```

Here are some of the `Array` methods you should work on learning:

- [`arr.forEach()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) - calls the provided function on each element in the array.
- [`arr.map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) - creates and returns a new array constructed by calling the provided function on each element of the original array.
- [`arr.find()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) - finds and returns an element from the array which matches a condition you define. See also [`arr.findLast()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLast), [`arr.findIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex), and [`arr.findLastIndex()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findLastIndex), which all work in similar ways.
- [`arr.filter()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) - creates and returns a new array containing only those elements that match a condition you define in your function.
- [`arr.every()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every) - returns `true` if all of the elements in the array meet a condition you define in your function.

There are more [`Array` methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Array_instances) you can learn as you progress with JavaScript, but these will get you started.

## Iterating over String, Array, and other collections

The most familiar way to iterate over a `String` or `Array` works as you'd expect:

```js
let s = 'Hello World!';
for (let i = 0; i < s.length; i++) {
  let char = s.charAt(i);
  console.log(i, char);
  // Prints:
  // 0, H
  // 1, e
  // 2, l
  // ...
}

let arr = [10, 20, 30, 40];
for (let i = 0; i < arr.length; i++) {
  let elem = arr[i];
  console.log(i, elem);
  // Prints:
  // 0, 10
  // 1, 20
  // 2, 30
  // ...
}
```

The standard `for` loop works, but is not the best we can do. Using a `for` loop
is prone to various types of errors: off-by-one errors, for example. It also
requires extra code to convert an index counter into an element.

An alternative approach is available in ES6, [`for...of`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of):

```js
let s = 'Hello World!';
for (let char of s) {
  console.log(char);
  // Prints:
  // H
  // e
  // l
  // ...
}

let arr = [10, 20, 30, 40];
for (let elem of arr) {
  console.log(elem);
  // Prints:
  // 10
  // 20
  // 30
  // ...
}
```

Using `for...of` we eliminate the need for a loop counter altogether, which has
the added benefit that we'll never under- or over- shoot our collection's element
list; we'll always loop across exactly the right number of elements within the
given collection.

The `for...of` loop works with all collection types, from `String` to `Array` to
`arguments` to `NodeList` (as well as newer collection types like
[`Map`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map),
[`Set`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), etc.).
