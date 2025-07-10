---
id: Events-Timers
title: Events & Timers
sidebar_position: 2
description: Events & Timers
---

# Events & Timers

## Events

The DOM relies heavily on a concept known as [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming).
In event-driven programs,
a main loop (aka the _event loop_), processes events as they occur.

Examples of events include things like user actions (clicking a button, moving the mouse,
pressing a key, changing tabs in the browser), or browser/code initiated actions (timers,
messages from background processes, reports from sensors).

Instead of writing a program in a strict order, we write functions that should be called
in response to various events occurring. Such functions are often referred to as
_event handlers_, because they handle the case of some event happening. If there is no
event handler for a given event, when it occurs the browser will simply ignore it. However,
if one or more event handlers are registered to listen for this event, the browser will
call each event handler's function in turn.

> You can think of events like light switches, and event handlers like light fixtures: flipping a light switch on or off triggers an action in the light fixture, or possibly in multiple light fixtures at once. The lights handle the event of the light switch being flipped.

DOM programming is typically done by writing many functions that execute in response
to events in the browser. We register our event handlers to indicate that we want a particular
action to occur. DOM events have a `name` we use to refer to them in code.

We can register a DOM event handler for a given event in one of two ways:

1. `element.onevent = function(e) {...};`
1. `element.addEventListener('event', function(e) {...})` and `element.removeEventListener('event', function(e) {...})`

In both cases above, we first need an HTML element. Events are emitted to a _target_ element.
Elements in the DOM can trigger one or more events, and we must know the name of the event we want
to handle.

In the first method above, `element.onevent = function(e) {...};`, a single event handler is registered
for the `event` event connected with the target element `element`. For example, `document.body.onclick = function(e) {...};`,
indicates we want to register an event handler for the `click` event on the `document.body` element (i.e., `<body>...</body>`).

In the second method above, use `addEventListener()` to add as many individual, separate event handlers as we need.
Whereas `element.onclick = function(e) {...};` binds a single event handler (function) to the `click` event for `element`,
using `element.addEventListener('click', function(e) {...});` _adds_ a new event handler (function) to any that might already
exist.

Consider the following code:

```js
let body = document.body;

function handleClick(e) {
  // Process the click event
}

function handleClick2(e) {
  // Another click handler
}

body.onclick = handleClick;
body.onclick = handleClick2;
// There is only 1 click event handler on body: handleClick2 has replaced handleClick.

body.addEventListener('click', handleClick);
body.addEventListener('click', handleClick2);
// There are now multiple, unique click handlers bound to the body's click event.
```

Because `addEventListener()` is more versatile than the older `onevent` properties, you are
encouraged to use it in most cases.

Here's an example of the first method, where we only need a single event handler.
In the following case, a web page has a Save button, and we want to save the user's
work when she clicks it.

```html
<button id="btn-save">Save</button>
<script>
  // Get a reference to our Save <button>
  let saveBtn = document.querySelector('#btn-save');

  function save() {
    // Save the user's work
  }

  // Register a single event handler on the save button's click event
  saveBtn.onclick = function (e) {
    // Save the user's work, calling a save() function we wrote elsewhere
    save();
  };
</script>
```

Now consider the same code, but with multiple event handlers. In this case
we not only want to save the user's work, but also log the information in our
web analytics so we can keep track of how popular this feature is (how many times
it gets clicked):

```html
<span id="needs-saving">Document has changes, Remember to Save!</span>
...
<button id="btn-save">Save</button>
<script>
  // Get a reference to our Save <button>
  let saveBtn = document.querySelector('#btn-save');

  // Register first event handler on the save button's click event
  saveBtn.addEventListener('click', function (e) {
    // Save the user's work, calling a save() function we wrote elsewhere
    save();

    // Remove the "needs to be saved" info showing in our UI, since we've saved
    document.querySelector('#btn-save').setAttribute('hidden', true);
  });

  // Register second event handler on the save button's click event
  saveBtn.addEventListener('click', function (e) {
    // Log some info to the console for debugging.
    console.log('[DEBUG] Save clicked');

    // Use an analytics Object (defined elsewhere) to update our count for this event
    analytics.increment('save');
  });
</script>
```

In this second example, it's possible for the browser to call more than one function
(event handler) in response to a single event (`click`). What's nice about this is that
different parts of our code don't have to be combined into a single function. Instead,
we can keep things separate (saving logic vs. analytics logic).

A complete example of a page that listens for changes to the network online/offline status,
and updates the page accordingly, is available at [online.html](files/online.html.txt).

## Common Events

There are [many types of events we can listen for in the DOM](https://developer.mozilla.org/en-US/docs/Web/Events),
some of which are very specialized to certain elements or Objects. However, there some common ones we'll use quite often:

- [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) - fired when a resource has finished loading (e.g., a `window`, `img`)
- [`beforeunload`](https://developer.mozilla.org/en-US/docs/Web/Events/beforeunload) - fired just before the window is about to be unloaded (closed)
- [`focus`](https://developer.mozilla.org/en-US/docs/Web/Events/focus) - when the element receives focus (cursor input)
- [`blur`](https://developer.mozilla.org/en-US/docs/Web/Events/blur) - when the element loses focus
- [`click`](https://developer.mozilla.org/en-US/docs/Web/Events/click) - when the user single clicks on an element
- [`dblclick`](https://developer.mozilla.org/en-US/docs/Web/Events/dblclick) - when the user double clicks on an element
- [`contextmenu`](https://developer.mozilla.org/en-US/docs/Web/Events/contextmenu) - when the right mouse button is clicked
- [`keypress`](https://developer.mozilla.org/en-US/docs/Web/Events/keypress) - when a key is pressed on the keyboard
- [`change`](https://developer.mozilla.org/en-US/docs/Web/Events/change) - when the content of an element changes (e.g., an input element in a form)
- [`mouseout`](https://developer.mozilla.org/en-US/docs/Web/Events/mouseout) - when the user moves the mouse outside the element
- [`mouseover`](https://developer.mozilla.org/en-US/docs/Web/Events/mouseover) - when the user moves the mouse over top of the element
- [`resize`](https://developer.mozilla.org/en-US/docs/Web/Events/resize) - when the element is resized

All of the events described above can be used in either of the two ways we discussed above.
For example, if we wanted to use the `mouseout` event on an element:

```html
<div id="map">...</div>
<script>
  let map = document.querySelector('map');

  // Method 1: register a single event handler via the on* property
  map.onmouseout = function (e) {
    // do something here in response to the mouseout event on this div.
  };

  // Method 2: register one of perhaps many event handlers via addEventListener
  map.addEventListener('mouseout', function (e) {
    // do something here in response to the mouseout event on this div.
  });
</script>
```

### The [`Event` Object](https://developer.mozilla.org/en-US/docs/Web/API/Event)

In the example code above, you may have noticed that our event handler functions often looked like this:

```js
element.onclick = function (e) {
  // e is an instance of the Event object
};
```

The single `e` argument is an instance of the [`Event` Object](https://developer.mozilla.org/en-US/docs/Web/API/Event).
The `e` or `event` is provided to our event handler function in order to pass information about the event, and to give
us a chance to alter what happens next.

For example, we can get a reference to the element to which the event was dispatched using
[`e.target`](https://developer.mozilla.org/en-US/docs/Web/API/Event/target). We can also instruct
the browser to prevent the "default" action from happening as a result of this event using
[`e.preventDefault()`](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault), or
stop the event from continuing to _bubble_ up the DOM (i.e., rise up the DOM tree nodes, triggering
other event handlers along the way) using [`e.stopPropagation()](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation).

Here's an example showing how to use these:

```html
<button id="btn">Click Me</button>
<script>
  document.querySelector('#btn').addEventListener('click', function (e) {
    // Prevent this event from doing anything more, we'll handle it all here.
    e.preventDefault();
    e.stopPropagation();

    // Get a reference to the <button> element
    let btn = e.target;

    // Change the text of the button
    btn.innerHTML = 'You clicked Me!';
  });
</script>
```

Some events also provide specialized (i.e., derived from `Event`) `event` Objects
with extra data on them related to the context of the event. For example, a [`MouseEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent)
gives extra detail whenever a click, mouse move, etc. event occurs:

```html
<div id="position"></div>
<script>
  document.body.addEventListener('click', function (e) {
    // Get extra info about this mouse event so we know where the pointer was
    let x = e.screenX;
    let y = e.screenY;

    // Display co-ordinates where the mouse was clicked: "Position (300, 342)"
    document.querySelector('#position').innerHTML = `Position (${x}, ${y})`;
  });
</script>
```

## Timers

It's also possible for us to write an event handler that happens in response to a timing event (delay) vs.
a user or browser event. Using these timing event handlers, we scheduling a task (function) to run after
a certain period of time has elapsed:

- `setTimeout(function, delayMS)` - schedule a task (`function`) to be run in the future (`delayMS` milliseconds from now). Can be cancelled with `clearTimeout(timerID)`
- `setInterval(function, delayMS)` - schedule a task (`function`) to be run in the future every `delayMS` milliseconds from now. Function will be called repeatedly. Can be cancelled with `clearInterval(timerID)`

Here's an example of using an `interval` to update a web page with the current date and time every 1 second.

```html
<p hidden>The current date and time is <time id="current-date"></time></p>
<button id="btn-start">Start Timer</button>
<button id="btn-end">End Timer</button>
<script>
  let startButton = document.querySelector('#btn-start');
  let endButton = document.querySelector('#btn-end');
  let timerId;

  // When the user clicks Start, start our timer
  startButton.onclick = function (e) {
    // If the user clicks it more than once, ignore it once it's running
    if (timerId) {
      return;
    }

    let currentDate = document.querySelector('#current-date');
    currentDate.removeAttribute('hidden');

    // Start our timer to update every 1000ms (1s), showing the current date/time.
    timerId = setInterval(function () {
      let now = new Date();
      currentDate.innerHTML = now.toLocaleString();
    }, 1000);
  };

  endButton.onclick = function (e) {
    // If the user clicks End when the timer isn't running, ignore it.
    if (!timerId) {
      return;
    }

    // Stop the timer
    clearInterval(timerId);
    timerId = null;
  };
</script>
```
