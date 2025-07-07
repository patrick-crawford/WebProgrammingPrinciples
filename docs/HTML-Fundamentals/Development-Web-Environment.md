---
id: Development-Web-Environment
title: Development Web Environment
sidebar_position: 1
description: Development Web Environment
---

# Running a Development Web Environment

Developing for the web requires at least 3 things pieces of software:

1. a proper code editor which, is aware of HTML, JavaScript, and CSS
1. a web client (i.e., browser), with developer and debugging tools
1. a web server, to serve your web pages over HTTP to a browser

## Code Editor

For our code editor, we will be using [Visual Studio Code](https://code.visualstudio.com/),
which is a free ([open source](https://github.com/Microsoft/vscode)) code editor created
and maintained by Microsoft. It also works on Windows, macOS, and Linux. Make
sure you have downloaded and installed it on all the computers you will use for
web development.

## Web Client

For our web client we will use the many web browsers we introduced in Week 1, namely:

- Google [Chrome](https://www.google.com/chrome/) for desktop and Android
- [Microsoft Edge](https://www.microsoft.com/en-ca/windows/microsoft-edge) and Internet Explorer (IE)
- Apple [Safari and Safari for iOS](https://www.apple.com/ca/safari/)
- [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/)
- [Opera](https://www.opera.com/)

There are many more, and you are highly encouraged to install as many as possible.

## Web Server

We will also need a **web server** to host our web pages and applications. Installing
and running a web server can be complicated. Industry-grade web servers like
[Apache](http://httpd.apache.org/) and [nginx](https://www.nginx.com/) are free
and can be installed and run on your local computer; however, they
are much more complicated and powerful than anything we will need for hosting
our initial web pages.

For our purposes, we will use one of the many simple node.js based HTTP servers. In order to
use them, do the following:

1. Make sure you have installed [node.js](https://nodejs.org/en/) on your computer.
1. In a terminal window, navigate to the directory that you want your web server to host. For example `cd my-website`
1. Now download and run a web server using the [npx](https://docs.npmjs.com/cli/v7/commands/npx) command.

For example, you can use the [serve](https://github.com/vercel/serve) web server like this:

```sh
cd my-website
npx serve
Need to install the following packages:
  serve@14.2.1
Ok to proceed? (y)

   ┌──────────────────────────────────────────┐
   │                                          │
   │   Serving!                               │
   │                                          │
   │   - Local:    http://localhost:3000      │
   │   - Network:  http://10.7.133.229:3000   │
   │                                          │
   │   Copied local address to clipboard!     │
   │                                          │
   └──────────────────────────────────────────┘
```

You can now open your web browser to `http://localhost:3000` and browser your files.
This uses the `http` protocol, and connects you to the special IP address
`127.0.0.1`, also known as [localhost](https://en.wikipedia.org/wiki/Localhost)
(i.e., you can also use `http://localhost:3000`). The localhost IP address always
refers to _this_ computer, and allows you to connect network clients to your own
machine. The final `:3000` portion of the URL is a port number. Together,
`http://127.0.0.1:3000` means _connect using HTTP to my local computer on port 3000._

_NOTE: the second External IP address will be different than the above, but 127.0.0.1 will always be correct._

When you are done testing your web site, stop the web server by pressing `CTRL-C`
in your terminal window. To run the server again, use `npx serve`.

## Suggested Readings

- [HTML: HyperText Markup Language on MDN](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics)
- [Learning HTML: Guides and Tutorials](https://developer.mozilla.org/en-US/docs/Learn/HTML)
- [HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference)
