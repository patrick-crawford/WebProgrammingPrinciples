---
id: Introduction
title: Introduction
sidebar_position: 1
description: Introduction
---

# Introduction

In languages like C, we are used to thinking about data types separately from the functions
that operate upon them. We declare variables to hold data in memory, and call functions passing them
variables as arguments to operate on their values.

In object-oriented languages like JavaScript, we are able to combine data and functionality into
higher order types, which both contain data and allow us to work with that data. In other words,
we can pass data around in a program, and all the functionality that works on that data travels with it.

Let's consider this idea by looking at strings in C vs. JavaScript. In C a string is
a null terminated (`\0`) array of `char` elements, for example:

```c
const char name1[31] = "My name is Arnold";
const char name2[31] = {'M','y',' ','n','a','m','e',' ','i','s',' ','A','r','n','o','l','d','\0'};
```

With C-style strings, we perform operations using standard library functions, for example `string.h`:

```c
#include <string.h>

int main(void)
{
    char str[31];        // declare a string
    ...
    strlen(str);         // find the length of a string str
    strcpy(str2, str);   // copy a string
    strcmp(str2, str);   // compare two strings
    strcat(str, "...");  // concatenate a string with another string
}
```

JavaScript also allows us to work with strings, but because JavaScript is an object-oriented language, a JavaScript [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) is an `Object` with various [properties and methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/prototype#Properties) we can use for working with text.

One way to think about `Object`s like `String` is to imagine combining a C-string's data type with the functions that operate on that data. Instead of needing to specify _which_ string we want to work with, all functions would operate a particular _instance_ of a string. Another way to look at this would be to imagine that the data and the functions for working with that data are combined into one more powerful type. If we could do this in C, we would be able to write code that looked more like this:

```c
String str = "Hello"; // declare a string

int len = str.len;    // get the length of str
str.cmp(str2);        // compare str and str2
str = str.cat("..."); // concatenate "..." onto str
```

In the made-up code above, the _data_ (`str`) is attached to functionality that we can call
via the `.*` notation. Using `str.*`, we no longer need to indicate to the functions which string
to work with: all string functions work on the string data to which they are attached.

This is very much how `String` and other `Object` types work in JavaScript. By combining
the string character data and functionality into one type (i.e., a `String`), we can
easily create and work with text in our programs.

Also, because we work with strings at a higher level of abstraction (i.e., not as arrays of `char`),
JavaScript deals with memory management for us, allowing our strings to grow or shrink at runtime.
