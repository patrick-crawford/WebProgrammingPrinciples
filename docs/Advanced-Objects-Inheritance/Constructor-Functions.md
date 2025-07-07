---
id: Constructor-Functions
title: Constructor Functions
sidebar_position: 2
description: Constructor Functions
---

# Constructor Functions

Sometimes we need to create lots of `Objects` that have the same layout. For example, we might
be defining lots of users in an application. All of our user `Objects` need to work the same way
so that we can pass them around within our program, to and from functions. Every `user` needs
to have the same set of properties and methods, so we decide to write a factory function that can
build our `user` `Objects` for us based on some data. We call such functions a `Constructor`:

```js
// Define a Constructor function, `User`
function User(id, name) {
  // Attach the id to an Object referenced by `this`
  this.id = id;
  // Attach the name to an Object referenced by `this`
  this.name = name;
}

// Create a new instance of a User (Object)
let user1 = new User(1, 'Sam Smith');
// Create another new instance of a User (Object)
let user2 = new User(2, 'Joan Winston');
```

Notice that unlike all previous functions we've defined, the `User` function starts with a
capital `U` instead of a lower case `u`. We use this naming convention to indicate that
`User` is special: a constructor function. A constructor function needs to be called with
the extra `new` keyword in front of it. When we say `new User(...)` we are saying,
_create a new object, and pass it along to User so it can attach various things to it_.

A constructor can also add methods to an object via `this`:

```js
// Define a Constructor function, `User`
function User(id, name) {
  this.id = id;
  this.name = name;

  // Add a toString method
  this.toString = function () {
    return `${this.name} (#${this.id})`;
  };
}

// Create a new instance of a User (Object)
let user1 = new User(1, 'Sam Smith');
console.log(user1.toString()); // 'Sam Smith (#1)
```

In the code above, we're creating a new function every time we create a new User. As we
start to create lots of users, we'll also be creating lots of duplicate functions. This will
cause our program to use more and more resources (memory), which can lead to issues as the
program scales.

## Object Prototypes

What we would really like is a way to separate the parts of a User that are different for each
user (the data: `id`, `name`), but somehow share the parts that are the same (the methods: `toString`).
JavaScript gives us a way to accomplish this via an `Object`'s `prototype`.

JavaScript is unique among programming languages in the way it accomplishes sharing
between `Object`s. All object-oriented languages provide some mechanism for us to share or
inherit things like methods in a type hierarchy. For example, C++ and Java use classes, which
can inherit from one another to define methods on parents vs. children.
JavaScript uses [_prototypal inheritance_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain) and a special property called `prototype`.

In JavaScript, we always talk about `Object`s, because every object is an instance of `Object`.
Notice the capital `O` in `Object`, which should give you an indication of what it is: a constructor
function. In a previous week we said that an `Array` is an `Object`, and a `RegExp` is an `Object`.
This is true because of JavaScript's type system, where almost everything is _chained_ to `Object`.

JavaScript objects always have a prototype, which is an object to which their `.prototype` property
refers. At runtime, when we refer to an object's property, JavaScript first looks for that property
on the object itself. If it doesn't find it, the prototype object is visited, and the same search is
done. The process continues until the end of the prototype chain is reached at `Object`.

Let's rewrite our `User` so that the `toString` method is moved from each user instance to the
prototype of all user instances:

```js
// Define a Constructor function, `User`
function User(id, name) {
  this.id = id;
  this.name = name;
}

User.prototype.toString = function () {
  return `${this.name} (#${this.id})`;
};
```

This code looks very similar to what we originally wrote. Notice that we've moved
`toString` out of the `User` function, and instead attached it to `User.prototype`.
By doing so, we'll only ever need a single copy of this function: every `new User()` instance
we create will also include a reference to a prototype object, which contains our function.
When we use `user1.toString()`, JavaScript will do something like this:

1. does `user1` have a property called `toString`? No, we didn't add one in the constructor.
2. does `user1.prototype` have a property called `toString`? Yes, use that.

What if we'd written `user1.something()`?

1. does `user1` have a property called `something`? No, we didn't add one in the constructor.
2. does `user1.prototype` have a property called `something`? No.
3. does `user1.prototype.prototype` (i.e., `Object`) have a property called `something`? No.
4. there are no more objects in the prototype chain, throw an error

```js
user1.something();
// TypeError: user1.something is not a function
```

Whenever a method is used on a prototype, we still pass the current instance so we can get access
to its data. Notice in our `User.prototype.toString` method, we still referred to `this`, which
will be the instance of our user, and give us access to the correct data (`name`, `id`).

> There are times when defining a method inside a constructor makes sense vs. putting it on the prototype. The prototype will only have access to _public properties_ of an object instance, meaning things you explicitly add to `this` and expose to the rest of your program. Sometimes we want to define some data, but _hide_ it from the rest of a program, so it can't be changed after it gets created. Consider the following example, which uses a _closure_ to retain access to a variable in the scope of the constructor without exposing it:

```js
function User(id, name) {
  this.id = id;
  this.name = name;

  // private variable within User function, not attached to `this`.
  // Normally this variable would go out of scope after User() completed;
  // however, we will use a closure function below to capture this scope.
  let createdAt = Date.now();

  // Return the number of ms this player has been playing
  this.playerAgeMS = function () {
    let currentTime = Date.now();

    // Access `createdAt` in the parent scope, which we retain via this closure function.
    // Calculate how many ms between createdAt and the current time.
    return currentTime - createdAt + ' ms';
  };
}

let user = new User(1, 'Tom');
// We can access the total time this player has existed, but not modify it.
console.log(user.playerAgeMS());
// displays "4183 ms"
console.log(user.playerAgeMS());
// displays "5287 ms"
```

## JavaScript's `class` and `Object`

For a long time, JavaScript didn't have any notion of a class. Most Object-Oriented languages are based on the idea of a class, but JavaScript only has runtime instances (i.e., `Object`s) and didn't need them.

In recent years, a new syntax has been added to JavaScript to allow those more familiar with traditional OOP style programming to define their `Object`s using a new `class` keyword.

Let's recreate our code above as a `class` in JavaScript:

```js
class User {
  id;
  name;

  constructor(id, name) {
    this.id = id;
    this.name = name;
  }

  toString() {
    return `${this.name} (#${this.id})`;
  }
}
```

This code still uses the same prototype technique we learned above above, but does so in a more familiar syntax.

We can even use other OOP features like inheritance:

```js
class Student extends User {
  email;

  constructor(id, name, email) {
    // Call the User() constructor to set the inherited properties
    super(id, name);
    this.email = email;
  }

  // Override the toString() method for a Student
  toString() {
    return `"${this.name}" <${this.email}>`;
  }
}

let student = new Student('10234134', 'Jen Hogan', 'jhogan@myseneca.ca');
console.log(student.id, student.name, student.email);
console.log(student.toString());
```
