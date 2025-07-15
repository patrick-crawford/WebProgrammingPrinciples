---
id: Advanced Techniques
title: Advanced Techniques
sidebar_position: 3
description: Advanced Techniques
---

# Advanced Techniques

## XHR and Cross-Origin Requests

It should be noted that we've been making requests to third-party web servers
in the example above. This is something that won't always work for all servers,
or all data types.

In the examples above, the servers were configured to allow [Cross-Origin
Resource Sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS).
By default, browsers maintain a sandbox around resources (scripts, images, data)
from one origin, and don't let it mix in unsafe ways with resources from other
origins.

In general, it's best to load data from the same origin as your page (i.e.,
the same web server). The so-called "Same Origin" policy states that you can't
load data from other origins. However, using CORS headers, servers and browsers
can allow this in some cases. In the examples above, the servers added a header
`Access-Control-Allow-Origin: *` to indicate that cross-origin requests were
OK.

If ever you are trying to use XHR to request data from a serer, and it won't work,
the problem is almost certainly related to CORS.

## Other Mechanisms for working with Data

While XHR is a historically popular choice for accessing data from web services,
in recent years a number of new APIs have also emerged that offer both similar
and enhanced capabilities. Discussing these in any detail is beyond the scope
of this course; however, it is important that you're aware of them, and look
out for opportunities to learn and use them in future courses and projects.

### `fetch()` API

The [`fetch()`API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) provides
JavaScript developers a rich set of objects and functions for working with
the entire HTTP network infrastructure, including things like [requests](https://developer.mozilla.org/en-US/docs/Web/API/Request), [responses](https://developer.mozilla.org/en-US/docs/Web/API/Response),
the [cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache), etc.
It uses the modern [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) API for handling callbacks.

Here's what it would look like to use `fetch` to request the current Bitcoin
value from our first example above:

```js
fetch('https://blockchain.info/q/24hrprice?cors=true')
  .then(function (response) {
    var currentValue = `${response.text()} (USD)`;
    updateBitcoinValue(currentValue);
  })
  .catch(function (err) {
    updateBitcoinValue('unknown (error, unable to get current value)');
  });
```

`fetch` offers much greater control over the network, and makes it easier to
process data coming from the server.

### Server Sent Events

With our Bitcoin example, we needed to constantly poll (i.e., re-request) the
updated value from the server. Another approach would be to wait for the server
to send us an update (push). One way to accomplish this is with [Server Sent Events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events).

Server Sent Events allow web sites to open a long running connection with a server, and get updates from the server when there is new data. On the browser
side, we use the [`EventSource`](https://developer.mozilla.org/en-US/docs/Web/API/EventSource) `Object` to process
these events, just as we would other types of events in a web page.

### Web Sockets

Server Sent Events are great for 1-way communciation from a server to a browser,
but sometimes we need to _also_ send data back to the server at regular intervals.
Consider a chat application, where we need to both receive and send messages.

In such systems, we need a bi-directional, long-running connection to the server.
The browser provides this in the form of a [`WebSocket`](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API). Web Sockets
can be connected to different backends written in any language. Within the browser, we receive events when data arrives, and send data when we need to over
the socket.

## Modern Front End Development

The concepts we've been discussing above have come to define the modern
approach to web development. Browsers have gotten faster and more powerful,
and the APIs and tools for building web services more full-featured.

As a result, new approaches to front-end development have taken over.
In your follow-up courses you'll learn more about popular front-end frameworks,
which build on the low-level ideas we've been using here (HTML, CSS, JS, DOM, JSON), for example:

- [React](https://reactjs.org/)
- [Angular](https://angular.io/)
- [Vue](https://vuejs.org/)
- [Ember](https://www.emberjs.com/)

These frameworks take a data-driven approach to developing on the web, separating
an applications data and state from its presentation. The ideas begun with AJAX
are taken to another level, and single-page HTML applications are used to create
rich interfaces.

Understanding the foundation for how all of this works, from HTML, CSS, and JS to JSON and XHR, will be an important part of taking the next step.
