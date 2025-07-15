---
id: AJAX-Fundamentals
title: AJAX Fundamentals
sidebar_position: 1
description: AJAX Fundamentals
---

# AJAX Fundamentals

## AJAX

AJAX is a term [coined in 2005 by Jesse James Garrett](http://adaptivepath.org/ideas/ajax-new-approach-web-applications/) that refers
to an approach to web development that uses dynamic requests to a server to
update portions of a page at runtime. Today, the method is so common that
it's hard to talk about it not existing. But at the time, it was a game changer.

AJAX stands for Asynchronous JavaScript and XML, which is based on a group of
web technologies: HTML (and at the time XHTML), CSS, JavaScript, the DOM, XML,
JSON, and a web API called [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), or just
XHR for short.

Before 2005, web browsers lacked a lot of the modern features we take for granted
today. Web servers were used to build and serve all (or most) aspects of a web
page. Making changes on the page meant a full request/response trip to and from
the server, in order to update content. The entire page had to be reloaded for
anything of significance to change.

Today we expect "real-time" data to be a part of our web browsing experience.
Consider a site like GMail or Google Maps. If we want to see messages in
another folder, or navigate to another city, we expect to be able to do that
without having to reload the entire page. AJAX makes this possible.

Instead of modifying the entire page (DOM), we instead make background requests
for data from servers, and then use that data to update the page's contents
live via the DOM's APIs.

## Understanding AJAX's "A" (Asynchronous) and "J" (JavaScript)

As we know from previous discussions, web browsers use HTTP/HTTPS to send
requests to web servers, which build replies and send back responses (HTML, CSS,
images, fonts, JavaScript, etc).

While we don't want to have to reload the entire page in order to get updates
from the server, we would like to be able to leverage this communication pattern
from within the running page: we need a way to make HTTP requests, wait for
responses from the server, and then do something with the data.

Browsers provide a mechanism for doing this in the form of the [`XMLHttpRequest`
Object](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), or
XHR for short. An XHR object let's us create and send HTTP requests to a server,
and get back data responses in various forms (XML, HTML, JSON, text, binary, etc.)

Our XHR requests happen in the background, asynchronously (without blocking the
main UI thread in the browser), so user's can continue to work and interact with
the page while we wait for a response.

Finally, we work with XHR via JavaScript code. Let's look at a very basic
example:

```js
// 1. Create a new instance of an XMLHttpRequest Object using its constructor
var xhr = new XMLHttpRequest();

// 2. Define an event handler for the `load` event, which happens when data arrives
xhr.onload = function () {
  // 3. Get the data from the `xhr` object's `responseText` property
  var data = this.responseText;
  console.log('data arrived', data);
};

// 4. Create an HTTP GET request to the given URL
xhr.open('GET', 'http://example.com');

// 5. Send the HTTP request to the server, and wait asynchronously for the reply
xhr.send();
```

## Example 1: Current Bitcoin Value in USD

To demonstrate a real-world example of what we've been discussing, let's
build a simple example. Imagine we want to create a web page that includes
information about the current market value of [Bitcoin](https://en.wikipedia.org/wiki/Bitcoin), the most famous of the blockchain-based
cryptocurrencies.

The website [https://www.blockchain.com](https://www.blockchain.com) provides a number of web services we can use to get this information. In particular,
we'll use [https://blockchain.info/q/24hrprice](https://blockchain.info/q/24hrprice), which gives the price in US dollars
over the past 24 hours.

Here's an (simplified) example of what it sends when we make an HTTP request:

```
HTTP/2 200
date: Sun, 02 Dec 2018 22:48:35 GMT
content-type: text/plain; charset=utf-8

4200.82
```

In the above response, we have HTTP headers, a blank line, and then the data: `4200.82`.

We want our web page to include this information, but then automatically update
it every minute by requesting the current value again over HTTP. Here's
one way we could do it.

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>Bitcoin Value</title>
  </head>
  <body>
    <p>Current Bitcoin value: <span id="bitcoin-value"></span></p>
    <script>
      function updateBitcoinValue(newValue) {
        // Update the <span> with the new value we get from the server
        var span = document.querySelector('#bitcoin-value');
        span.innerHTML = newValue;

        // Every minute, get the new value and update the page
        var oneMinute = 60 * 1000;
        setTimeout(getCurrentValue, oneMinute);
      }

      function getCurrentValue() {
        var xhr = new XMLHttpRequest();
        var url = 'https://blockchain.info/q/24hrprice?cors=true';

        // If/When the request returns successfully, get the value and update DOM
        xhr.onload = function () {
          // Format the raw text we get from the server into a currency string
          var response = this.responseText;
          var currentValue = `${response} (USD)`;
          updateBitcoinValue(currentValue);
        };

        // If the request fails, and we get an error, update the page with an error message
        xhr.onerror = function (e) {
          updateBitcoinValue('unknown (error, unable to get current value)');
        };

        // Open a GET request to the Blockchain API
        xhr.open('GET', url);

        // Send our HTTP request to the server, and wait for a response
        xhr.send();
      }

      window.onload = function () {
        getCurrentValue();
      };
    </script>
  </body>
</html>
```

By separating the data into a separate web service, it's possible for various
applications to all share it, and use it in different ways.

## Suggested Readings

- [AJAX Guide](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX)
- [Working with JSON](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
- [Using XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest)
