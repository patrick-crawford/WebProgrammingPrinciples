---
id: Objects-JavaScript
title: Objects in JavaScript
sidebar_position: 1
description: Objects in JavaScript
---

# Objects in JavaScript

So far we've been working with built-in `Objects` in JavaScript. We can also create
our own in order to model complex data types in our programs. There are a number
of ways to do this, and we'll look at a few of them now.

An `Object` in JavaScript is a _map_ (also known as an _associative array_ or a _dictionary_),
which is a data structure composed of a collection of _key_ and _value_ pairs. We call an `Object`'s key/value pairs _properties_. Imagine a JavaScript `Object` as a dynamic "bag" of properties, a
property-bag. Each _key_ is a unique `String`, and an `Object` can only contain a given _key_ once. An `Object` can have any number of _properties_, and they can be added and removed at runtime.

Much like we did with an `Array` or `RegExp`, we can create instances of `Objects`
via literals. An `Object` literal always starts with `{` and ends with `}`. In between these curly
braces we can optionally include a list of any properties (comma separated) we want to attach to this `Object` instance. These properties are written using a standard `key: value` style, with the property's name `String` coming first, followed by a `:`, then its value. The value can be any JavaScript value, including functions or other `Objects`.

Here are a few examples:

```js
// an empty Object, with no properties
let o = {};

// a `person` Object, with one property, `name`
let person = { name: 'Tim Wu' };

// a `campus` Object, with `name` as well as co-ordinates (`lat`, `lng`).
// NOTE: as the Object literal gets longer, we break it into multiple lines.
let campus = {
  name: 'Seneca@York',
  lat: 43.7714,
  lng: -79.4988,
};

// a `menu` Object, which contains lists of menu items per meal
let menu = {
  breakfast: ['eggs', 'toast', 'banana', 'coffee'],
  lunch: ['salad', 'chicken', 'apple', 'milk'],
  dinner: ['salmon', 'rice', 'green beans'],
};
```

## Accessing Elements in an Object

`Object` property names are `String`s, and we can refer to them either via the _dot operator_ `.name`,
or using the _bracket operator_ `['name']` (similar to indexing in an `Array`):

```js
let person = { name: 'Tim Wu' };

// get the value of the `name` property using the . operator
console.log(person.name);

// get the value of the `name` property using the [] operator
console.log(person['name']);
```

> Why would you choose the dot operator over the bracket operator, or vice versa? The dot operator is probably more commonly used; however, the bracket operator is useful in a number of scenarios. First, if you need to use a reserved JavaScript keyword for your property key, you'll need to refer to it as a string (e.g., `obj['for']`). Second, it's sometimes useful to be able to pass a variable in order to lookup a property value for a name that will be different at runtime. For example, if you are using usernames as keys, you might do `users[currentUsername]`, where `currentUsername` is a variable holding a `String` for the logged in user.

### Destructuring Objects

In the same way that we _destructured_ `Array` values into new variables, we can also use the same
technique with an `Object`. Recall that JavaScript allows us to [Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to unpack values in an `Array` or `Object` into distinct variables. Consider each of the following methods, both of which accomplish the same goal:

With an `Array`, we learned that you can _destructure_ various elements into new variables:

```js
// Co-ordinates for Seneca's Newnham Campus
let position = [43.796, -79.3486];

let [lat, lng] = position;
```

The same can be done with an `Object`. Imagine a complex `Object`, with lots of properties, but we're only interested in a few of them:

```js
let senecaNewnham = {
  address: '1750 Finch Ave. East',
  city: 'Toronto',
  province: 'Ontario',
  postalCode: 'M2J 2X5',
  phoneNumber: '416.491.5050',
  lat: 43.796,
  lng: -79.3486,
};

// Destructure only the `lat` and `lng` properties
let { lat, lng } = senecaNewnham;
```

This is a powerful technique for extracting data from an `Object`.

## Modifying Object Properties

`Object` literals allow us to define an initial set of properties on an `Object`, but we aren't
limited to that set. We can easily add new ones:

```js
let data = {};

data.score = 17;
data.level = 3;
data.health = '***';
```

Here we define an empty `Object`, but then add new properties. Because we can add properties
after an `Object` is created, we always have to deal with a property not existing. If we try to access
a property that does not exist on an `Object`, there won't be an error. Instead, we will get back
`undefined` for its value:

```js
let currentScore = data.score; // `score` exists on `data`, and we get back the value `17`
let inventory = data.inventory; // `inventory` does not exist on `data`, so we get back `undefined`
```

Because properties may or may not exist at runtime, it's important to always check for a value
before trying to use it. We could rewrite the above to first check if `data` has an `inventory`
property:

```js
if (data.inventory) {
  // `data` has a value for `inventory`, use data.inventory here...
} else {
  // there is no `inventory` on `data`, do something else...
}
```

Another common situation where you have to deal with this is working with deep structures. Consider
an `Object` that defines the structure of a level in a video game. The level includes various `rooms`,
some of which contain a `monster`:

```js
let gameLevel = {
  name: 'Level 1',
  rooms: {
    // Each room has a unique ID
    R31343: {
      name: 'Front Hallway',
    },
    R31344: {
      name: 'Kitchen',
      monster: {
        name: 'Bear',
        strength: 15,
      },
    },
    R31345: {
      name: 'Back Hallway',
    },
    R31346: {
      name: 'Sitting Room',
      monster: {
        name: 'Dog',
        strength: 8,
      },
    },
  },
};
```

When working this code, we can access a particular room by its `ID`:

```js
// Get a reference to the Kitchen
let room = gameLevel.rooms.R31344;
```

However, we used an `ID` that doesn't exist, we'd get back `undefined`:

```js
// Get a reference to the TV Room (no such room!)
let room = gameLevel.rooms.R31347; // <-- room is `undefined`
```

If we then try to access the `monster` in that room, our program will crash:

```js
let room = gameLevel.rooms.R31347; // <-- room is `undefined`
console.log(room.monster); // <-- crash! room is `undefined` so we can't access `monster within it
```

JavaScript provides a few ways to deal with this problem. Consider:

```js
let room = gameLevel.rooms.R31347;

// Version 1
if (room) {
  // only access room if it is truthy
}

// Version 2
if (room && room.monster) {
  // only try to get .monster if room is truthy
}

// Version 3
if (room?.monster) {
  // same as 2, but using ?. syntax
}
```

In the third version above we've used [optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining) via the `?.` operator. This stops us from going any further in an object chain, when something is undefined.

## Using Objects: dealing with optional parameters

A very common pattern in JavaScript programs that uses this concept is optional argument
passing to functions. Instead of using an unknown number of `arguments` for a function, we
often use an `options` `Object`, which may contain values to be used in the function. Consider
the case of starting a game and sometimes passing existing user data:

```js
// Make sure `options` exists, and use an empty `Object` instead if it's missing.
// If we don't do this, we'll get an error if we try to do `options.score`, since
// we can't lookup the `score` property on `undefined`.
function initGame(options = {}) {
  // If the user already has a score, use that, otherwise default to 0
  let score = options.score || 0;
  // If the user is already on a level, use that, otherwise default to 1
  let level = options.level || 1;
  // If the user has collected an items in her inventory, use that, otherwise an empty Array
  let inventory = options.inventory || [];

  // Begin the game, passing the values we have determined above
  playGame(score, level, inventory);
}

// Define our options: we have a score and level, but no inventory
let options = {
  score: 25,
  level: 2,
};
initGame(options);
```

In the code above, we have an `options` `Object` that defines some, but not all of the
properties our `initGame` function might use. We wrote `initGame` using a single argument
so that it was easier to call: we didn't need to worry about the order or number of arguments,
and could instead just define an `Object` with all of the properties we had. The `initGame`
function examined the `options` at runtime to see which properties existed, and which were
`undefined` and needed a default value instead. Recall that we can use the _logical OR_ (`||`)
operator to choose between two values at runtime.

It's also common to see people use _destructuring_ here:

```js
function processStudent(student) {
  let { name, studentId, username, email } = student;
  // Use values destructured from student object
}

processStudent({
  name: 'Tim Wu',
  studentId: '10341346',
  username: 'timw',
  email: 'timw@myseneca.ca',
});
```

The value of what we've done above is that passing many arguments to a function is easier when we can name them as properties on an `Object` instead of having to pass them positionally as arguments.

## Updating, Clearing, and Removing properties

We've seen that properties can be defined when declared as part of a literal and
added later via the `.` or `[]` operators. We can also update or remove values
after they are created:

```js
let o = {};

// Add a name property
o.name = 'Tim Wu';

// Update the name property to a new value, removing the old one.
o.name = 'Mr. Timothy Wu';
```

An `Object`'s property keys are unique, and setting a value for `o.name` more than once
doesn't add more properties--it overwrites the value already stored in the existing property.
We can also _clear_ (remove the value but not the key) or _delete_ (remove the entire property
from the object, key and value) things from an `Object`.

```js
let o = {};

// Add a `height` property
o.height = '35 inches';

// Add an owner ID property
o.owner = '012341341';

// Clear the value of `height`. We leave the `height` key, but get rid of the '35 inches' value
o.height = null;

// Completely remove the owner property from the object (both the key and its value)
delete o.owner;
```

> Why would you choose to assign `null` vs. use `delete`? Often we want to get rid of a key's value, but will use the key again in the future (e.g., add a new value). In such cases we just _null the value_ by assigning the key a value of `null`. If we know that we'll never use this key again, and we don't want to retain it on the `Object`, we can instead completely remove the property (key and value) with `delete`. You'll see both used. For the most part, setting a key's value to `null` is probably what you want.

## Using Objects: creating sets to track arbitrary lists

Another common use of `Object`s, and their unique property keys, is to keep track of a sets, for example
to count or keep track of an unknown number of items. Consider the following program, which tracks how many times each
character appears within a `String`. The code uses the `[]` operator to allow for the keys to be created
and accessed via a variable (`char`). Without an `Object` we would have to hard-code variables for each
separate letter.

```js
// An empty `Object`, which we'll populate with keys (letters) and values (counts)
let characterCounts = {};

let sentence = 'The quick brown fox jumped over the lazy dog.';
let char;
let count;

// Loop through all characters in sentence
for (let char of sentence) {
  // Get the current count for this character, or use 0 if we haven't seen it before
  count = characterCounts[char] || 0;
  // Increase the count by 1, and store it in our object
  characterCounts[char] = count + 1;
}

console.log(characterCounts);
/* Our characterCounts Object now looks like this, and there were 8 spaces, 2 'h's, etc:
{ T: 1,
  h: 2,
  e: 4,
  ' ': 8,
  q: 1,
  u: 2,
  i: 1,
  c: 1,
  k: 1,
  b: 1,
  r: 2,
  o: 4,
  w: 1,
  n: 1,
  f: 1,
  x: 1,
  j: 1,
  m: 1,
  p: 1,
  d: 2,
  v: 1,
  t: 1,
  l: 1,
  a: 1,
  z: 1,
  y: 1,
  g: 1,
  '.': 1 }
*/
```

## Complex Property Types: `Object`, `Function`

We said earlier that `Object` properties can be any valid JavaScript type. That includes
`Number`, `String`, `Boolean`, etc., also `Object` and `Function`. A property may define
a complex `Object` of its own:

```js
let part = {
  id: 5,
  info: {
    name: 'inner gasket',
    shelf: 56713,
    ref: [5618, 5693],
  },
};
```

Here we define a `part`, which has an id (`part.id`) as well as a complex property named `info`,
which is itself an `Object`. We access properties deep in an `Object` the same way as a simple
property, for example: `part.info.ref.length` means: get the `length` of the `ref` array on the
`info` property of the `part` `Object`. An `Object`'s properties can be `Object`s many levels
deep, and we use the `.` or `[]` operators to access these child properties.

An `Object` property can also be a function. We call these functions _methods_. A _method_ has
access to other properties on the `Object` via the `this` keyword, which refers to the current
`Object` instance itself. Let's add a `toString()` method to our `part` `Object` above:

```js
let part = {
  id: 5,
  info: {
    name: 'inner gasket',
    shelf: 56713,
    ref: [5618, 5693],
  },
  toString: function () {
    return `${this.info.name} (#${this.id})`;
  },
};

console.log(part.toString()); // prints "inner gasket (#5)" to the console.
```

The `toString` property is just like any other key we've added previously, except its value
is an _anonymous function_. Just as we previously bound function expressions to variables,
here a function expression is bound to an `Object`'s property. When we write `part.toString` we
are accessing the function stored at this key, and by adding the `()` operator, we can invoke it:
`part.toString()` says _get the function stored at part.toString and call it_. Our function
accesses other properties on the `part` `Object` by using `this.*` instead of `part.*`. When the
function is run, `this` will be the same as `part` (i.e., a reference to _this_ `Object` instance).

> The [`this` keyword in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) is used in different contexts, and has a different meaning depending on where and how it is used. We will return to `this` and its various meanings throughout the course.

## Suggested Readings

- [Object-oriented JavaScript for beginners](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object-oriented_JS)
- [ExploringJS, Chapter 17. Objects and Inheritance](http://exploringjs.com/es5/ch17.html)
- [ExploringJS, Chapter 20. Dates](http://exploringjs.com/es5/ch20.html)
- [ExploringJS, Chapter 21. Math](http://exploringjs.com/es5/ch21.html)
