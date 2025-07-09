---
id: DOM-Introduction
title: DOM Introduction
sidebar_position: 1
description: DOM Introduction
---

# DOM Introduction

## From HTML to the DOM

Web pages rely on HTML for their initial structure and content. We write web pages using HTML,
and then use web browsers to parse and render that HTML into a living (i.e., modifiable at runtime)
tree structure. Consider the following HTML web page:

The DOM Tree is a living version of our HTML.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>This is a Document!</title>
    <meta charset="utf-8" />
  </head>
  <body>
    <h1>Welcome!</h1>
    <p>This is a paragraph with a <a href="index.html">link</a> in it.</p>
    <ul>
      <li>first item</li>
      <li>second item</li>
      <li>third item</li>
    </ul>
  </body>
</html>
```

The browser will parse and render this into a tree of nodes, the [DOM Tree](https://en.wikipedia.org/wiki/Document_Object_Model):

![DOM Tree for our HTML](/img/dom-tree.png)

The DOM Tree is made up of DOM Nodes, which represent all aspects of our document,
from elements to attributes and comments. We'll refer to nodes and elements interchangeably,
because all elements are nodes in the tree. However, there are also other types of nodes,
for example: text nodes (the text in a block element) and attribute nodes (key/value pairs).
We don't always show every node in our diagrams. Consider the `<p>` element from the example
above:

```html
<p>This is a paragraph with a <a href="index.html">link</a> in it.</p>
```

Here are the nodes that would be created:

![DOM Nodes in our p example](/img/p-node.png)

In this diagram, the gray, square boxes represent element nodes, while the white, rounded boxes are text nodes.

When we load a web page in a web browser, we see its fully parsed and rendered form.
The web browser _begins_ with the initial content we provide in our HTML. We can see the
initial source HTML for any page we visit, whether we authored it or not:

![View Source in Browser](/img/view-source.gif)

Our DOM Tree gets its name because of its shape: a _root_ element connected to _child_ nodes that extend
like the branches of a tree. This tree structure is how the browser views our web page,
and is why it is so important for us to open and close our HTML tags in order (i.e., our tags
define the structure of the tree that the browser will create at runtime).

As web developers we can see and interact with the DOM tree for a page using the browser's
built-in developer tools:

![Element Inspector in Dev Tools](/img/inspect.gif)

The dev tools allow us to [view and work with](https://developers.google.com/web/tools/chrome-devtools/beginners/html)
the parsed DOM elements in a page. We can also use the dev tools to visually select
an element in the page, and find its associated DOM element:

![Find Individual Elements in a Web Page](/img/inspect-element.gif)

> NOTE: it's a good idea to get experience using, and learn about your browser's dev tools so that you can debug and understand when things go wrong while you are doing web development. There are a number of guides to help you learn, like [this one from Google](https://developers.google.com/web/tools/chrome-devtools/).

## Programming the DOM

Web pages are dynamic: they can change in response to user actions, different data,
JavaScript code, etc. Where HTML defines the initial structure and content of a page,
the DOM is the _current_ or _actual_ content of the page as it exists right now in your browser.
And this can mean something quite different from the initial HTML used to load the page.

Consider a web page like GMail (or another email web client). When you visit your Inbox, the
messages you see are not the same as when your friend visits hers. The HTML for GMail is the same
no matter who loads the page. But it quickly changes in response to the needs of the current user.

So how does one modify a web page after it's been rendered in the browser? The answer is DOM programming.
We've been using this "DOM" acronym without defining it, and its high time we did.

The [Document Object Model (DOM)](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) is a programming interface (i.e., set of Objects, functions, properties) allowing scripts to interact with, and modify documents (HTML, XML). The DOM is an object-oriented representation of a web page. Client-side web programming is essentially _using_ the DOM via JavaScript to make web pages _do_ things or _respond_ to actions (e.g., user actions).

You may have noticed in our work with JavaScript that there was nothing particularly "webby" about
it as a language: we wrote functions, worked with arrays, created objects. Lots of programming
languages let you do this. JavaScript can't do anything with the web on its own. Instead, we need
to access and use the Objects, functions, and properties made available to us by the DOM using JavaScript.

As web programmers we use the DOM via JavaScript to accomplish a number of important tasks:

1. Finding and getting references to elements in the page
1. Creating, adding, and removing elements from the DOM tree
1. Inspecting and modifying elements and their content
1. Run code in response to events triggered by the user, browser, or other parts of our code

Let's look at each one in turn.

### Finding elements in the DOM with JavaScript

Our entry point to the DOM from JavaScript is via the global variable [`window`](https://developer.mozilla.org/en-US/docs/Web/API/Window).
Every web page runs in an environment created by the browser, and that environment includes
a global variable named [`window`](https://developer.mozilla.org/en-US/docs/Glossary/Global_object#window_object_in_the_Browser),
which is provided by the browser (i.e., we don't create it).

There are hundreds of Objects, methods, and properties available to our JavaScript code
via `window`. One example is [`window.document`](https://developer.mozilla.org/en-US/docs/Web/API/Document),
which is how we access the DOM in our code:

```js
// Access the document object for our web page, which is in the current window
let document = window.document;
```

> NOTE: since properties like `document` are available on the global `window` object, it is common to simply write `document` instead of `window.document`, since the global object is implied if no other scope is given.

Our document's tree of elements are now accessible to us, and we can access a number of
well-known elements by name, for example:

```js
// Get the value of the document's <title>
let title = document.title;

// Return a reference to the document's <body> element
let body = document.body;

// Return a list of all <a> elements in the document
let hyperlinks = document.links;

// Return a list of all the <img> elements in the document
let images = document.images;
```

There are lots more. We can easily experiment with these in the dev tools web console,
where we can access our `window` object. For example, here is the web page
[https://unsplash.com/search/photos/toronto](https://unsplash.com/search/photos/toronto) with the
web console open, and the result of `window.document.images` is shown, 41 `<img>` elements
are returned in a collection:

![window.document.images via the Web Console](/img/window-document-images.png)

We can also use a number of methods to search for and get a reference to one or more
elements in our document:

- [`document.getElementById(id)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById) - returns an element whose `id` attribute/property has the given `id` `String`
  ```html
  <div id="menu">...</div>
  <script>
    let menuDiv = document.getElementById('menu');
  </script>
  ```
- [`document.querySelector(selectors)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector) - similar to `document.getElementById(id)`, but also allows querying the DOM using [CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors) for an element that doesn't have a unique id:
  ```html
  <div id="menu">
    <p class="formatted">...</p>
  </div>
  <script>
    // We can specify we want to query by ID using a leading #
    let menuDiv = document.querySelector('#menu');
    // We can specify we want to query by CLASS name using a leading .
    let para = document.querySelector('.formatted');
  </script>
  ```
- [`document.querySelectorAll(selectors)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll) - similar to `document.querySelector(selector)`, but returns _all_ elements that match the selectors as a [`NodeList`](https://developer.mozilla.org/en-US/docs/Web/API/NodeList):
  ```html
  <div id="menu">
    <p class="formatted">Paragraph 1...</p>
    <p class="formatted">Paragraph 2...</p>
    <p class="formatted">Paragraph 3...</p>
  </div>
  <script>
    // Get all <p> elements in the document as a list
    let pElements = document.querySelectorAll('p');
    // Loop through all returned <p> elements in our list
    pElements.forEach(function (p) {
      // p is one of the returned <p> elements
    });
  </script>
  ```

These four methods will work in any situation where you need to get a reference to
something in document. In fact, you could rely solely on `document.querySelector()` and
`document.querySelectorAll()`, which cover the same functionality as a number of other
DOM methods:

```js
// The following two lines of code do exactly the same thing.
// NOTE the use of # to indicate `demo` is an id in the second example.
let elem = document.getElementById('demo');
let elem = document.querySelector('#demo');
```

### Creating elements and Modifying the DOM with JavaScript

In addition to searching through the DOM using JavaScript, we can also make changes to it. The DOM provides a number
of methods that allow use to create new content:

- [`document.createElement(name)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) - creates and returns a new element of the type specified by `name`.
  ```js
  let paragraphElement = document.createElement('p');
  let imageElement = document.createElement('img');
  ```
- [`document.createTextNode(text)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode) - creates a text node (the text within an element vs. the element itself).
  ```js
  let textNode = document.createTextNode('This is some text to show in an element');
  ```

These methods create the new nodes, but do not place them into the page. To do that, we first need to find
the correct position within the existing DOM tree, and then add our new node. We have to be clear _where_ we want
the new element to get placed in the DOM.

For example, if we want to place a node at the end of the `<body>`, we could use `.appendChild()`:

```js
let paragraphElement = document.createElement('p');
document.body.appendChild(paragraphElement);
```

If we instead wanted to place it within an existing `<div id="content">`, we'd do this:

```js
let paragraphElement = document.createElement('p');
let contentDiv = document.querySelector('#content');
contentDiv.appendChild(paragraphElement);
```

Both examples work the same way: given a parent node (`document` or `<div id="content">`), add
(append to the end of the list of children) our new element.

We can also use `.insertBefore(new, old)` to accomplish something similar: add our new node before
the `old` (existing) node in the DOM:

```js
let paragraphElement = document.createElement('p');
let contentDiv = document.querySelector('#content');
let firstDivParagraph = contentDiv.querySelector('p');
contentDiv.insertBefore(paragraphElement, firstDivParagraph);
```

Removing a node is similar, and uses `removeChild()`:

```js
// Remove a loading spinner
let loadingSpinner = document.querySelector('#loading-spinner');
// Get a reference to the loading spinner's parent element
let parent = loadingSpinner.parentNode;
parent.removeChild(loadingSpinner);
```

### Examples

1. Add a new heading to a document

   ```js
   // Create a new <h2> element
   let newHeading = document.createElement('h2');

   // Add some text to the <h2> element we just created.
   // Similar to doing <h2>This is a heading</h2>.
   let textNode = document.createTextNode('This is a heading');
   // Add the textNode to the heading's child list
   newHeading.appendChild(textNode);

   // Insert our heading into the document, at the end of <body>
   document.body.appendChild(newHeading);
   ```

1. Create a new paragraph and insert into the document

   ```html
   <div id="demo"></div>
   <script>
     // Create a <p> element
     let pElem = document.createElement('p');

     // Use .innerHTML to create text nodes inside our <p>...</p>
     pElem.innerHTML = 'This is a paragraph.';

     // Get a reference to our <div> with id = demo
     let demoDiv = document.querySelector('#demo');

     // Append our <p> element to the <div>
     demoDiv.appendChild(pElem);
   </script>
   ```

### Inspecting, Modifying a DOM element with JavaScript

Once we have a reference to an element in JavaScript, we use a number of properties and methods to
work with it.

### [Element Properties](https://developer.mozilla.org/en-US/docs/Web/API/Element#Properties)

- `element.id` - the `id` of the element. For example: `<p id="intro"></p>` has an `id` of `"intro"`.
- `element.innerHTML` - gets or sets the markup contained within the element, which could be text, but could also include other HTML tags.
- `element.parentNode` - gets a reference to the parent `node` of this element in the DOM.
- `element.nextSibling` - gets a reference to the sibling element of this element, if any.
- `element.className` - gets or sets the value of the `class` attribute for the element.

### [Element Methods](https://developer.mozilla.org/en-US/docs/Web/API/Element#Methods)

- `element.querySelector()` - same as `document.querySelector()`, but begins searching from `element` vs. `document`
- `element.querySelectorAll()` - same as `document.querySelectorAll()`, but begins searching from `element` vs. `document`
- `element.scrollIntoView()` - scrolls the page until the element is in view.

- `element.hasAttribute(name)` - checks if the attribute `name` exists on this `element`
- `element.getAttribute(name)` - gets the value of the attribute `name` on this `element`
- `element.setAttribute(name, value)` - sets the `value` of the attribute `name` on this `element`
- `element.removeAttribute(name)` - removes the attribute `name` from this `element`

### Examples

1. Reveal an error message in the page, by removing an element's `hidden` attribute
   ```html
   <!-- The `hidden` attribute means this <div> won't be displayed until it's removed -->
   <div id="error-message" hidden>
     <p>There was an error saving the document. Please try again!</p>
   </div>
   <script>
     // Try to save the file, and
     let error = saveFile();
     if (error) {
       let elem = document.querySelector('#error-message');
       elem.removeAttribute('hidden');
     }
   </script>
   ```
1. Insert a user's profile picture into the page

   ```js
   // Insert the user's picture (e.g., in response to hovering over a username)
   let profilePic = document.createElement('img');

   // Set attributes via getters/setters on the element vs. attributes
   profilePic.id = 'user-' + username;
   profilePic.height = 50;
   profilePic.src = './images/' + username + '-user-profile.jpg';

   // Insert the profile pic <img> into the document
   document.body.appendChild(profilePic);

   // Make sure the new image is visible, or scroll until it is
   profilePic.scrollIntoView();
   ```

1. Add new paragraph elements to a div

   ```js
   // Use .innerHTML as a getter and setter to update some text
   let elem = document.querySelector('#text');

   elem.innerHTML = '<p>This is a paragraph</p>';
   elem.innerHTML = elem.innerHTML + '<p>This is another paragraph</p>';
   ```
