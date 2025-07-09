---
id: HTML-Elements
title: HTML Elements
sidebar_position: 1
description: HTML Elements
---

# HTML Elements

## HTML Element Types: Block vs. Inline

Visual HTML elements are categorized into one of two groups:

1. [Block-level elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Block-level_elements): create a "block" of content in a page, with an empty line before and after them. Block elements fill the width of their parent element. Block elements can contain other block elements, inline elements, or text.
1. [Inline elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements): creates "inline" content, which is part of the containing block. Inline elements can contain other inline elements or text.

Consider the following HTML content:

```html
<body>
  <p>The <em>cow</em> jumped over the <b>moon</b>.</p>
</body>
```

Here we have a `<p>` paragraph element. Because it is a block-level element, this paragraph will
fill its container (in this case the `<body>` element). It will also have empty space added above and below it.

Within this block, we also encounter a number of other inline elements. First, we have simple text.
However, we also see the `<em>` and `<b>` elements being used. These will affect their content, but not
create a new block; rather, they will continue to flow inline in their container (the `<p>` element).

## Empty Elements

Many of the elements we've seen so far begin with an opening tag, and end with a closing tag: `<body></body>`.
However, not all elements need to be closed. Some elements have no _content_, and therefore don't need
to have a closing tag. We call these [empty elements](https://developer.mozilla.org/en-US/docs/Glossary/Empty_element).

An example is the [`<br>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/br) line break element.
We use a `<br>` when we want to tell the browser to insert a newline (similar to using `\n` in C):

```html
<p>Knock, Knock<br />Who's there?</p>
```

Other examples of empty elements include `<hr>` (for a horizontal line), `<meta>` for including metadata
in the `<head>`, and [a dozen others](https://developer.mozilla.org/en-US/docs/Glossary/Empty_element).

## Grouping Elements

Often we need to group elements in our page together. We have a number of pre-defined element container options for how to achieve this, depending on what kind of content we are creating, and where it is in the document.

Using this so-called semantic markup helps the browser and other tools (e.g., accessibility) determine important structural information about the document (see [this post](https://www.brucelawson.co.uk/2018/the-practical-value-of-semantic-html/) for a great discussion):

- [`<header>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header) - introductory material at the top of a
- [`<nav>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/nav) - content related to navigation (a menu, index, links, etc)
- [`<main>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/main) - the main content of the document.
- [`<article>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/article) - a self-contained composition, such as a blog post, article, etc.
- [`<section>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) - a group of related elements in a document representing one section of a whole
- [`<footer>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer) - end material (author, copyright, links)

Sometimes there is no appropriate semantic container element for our content, and we need something more generic.
In such cases we have two options:

- [`<div>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div) - a generic block-level container
- [`<span>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/span) - a generic inline container

```html
<div>
  <p>
    This is an example of a using a div element. It also includes this
    <span><em>span</em> element</span>.
  </p>
  <p>
    Later we'll use a div or span like this to target content in our page with JavaScript or CSS
    styles.
  </p>
  <p></p>
</div>
```

## Tables

Sometimes our data is tabular in nature, and we need to present it in a grid. A number of elements are used to create them:

- [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) - the root of a table in HTML
- [`<caption>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/caption) - the optional title (or caption) of the table
- [`<thead>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/thead) - row(s) at the top of the table (header row or rows)
- [`<tbody>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tbody) - rows that form the main body of the table (the table's content rows)
- [`<tfoot>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tfoot) - row(s) at the bottom of the table (footer row or rows)

We define rows and columns of data within the above using the following:

- [`<tr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tr) - a single row in a table
- [`<td>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) - a single cell (row/column intersection) that contains table data
- [`<th>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th) - a header (e.g., a title for a column)

We can use the `rowspan` and `colspan` attributes to extend table elements beyond their usual bounds,
for example: have an element span two columns (`colspan="2"`) or have a heading span 3 rows (`rowspan="3")`.

```html
<table>
  <caption>
    Order Information
  </caption>

  <thead>
    <tr>
      <th>Quantity</th>
      <th>Colour</th>
      <th>Price (CAD)</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>1</td>
      <td>Red</td>
      <td>$5.60</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Blue</td>
      <td>$3.00</td>
    </tr>
    <tr>
      <td>8</td>
      <td>Blue</td>
      <td>$1.50</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <th colspan="2">Total</th>
      <th>$26.60</th>
    </tr>
  </tfoot>
</table>
```

## Suggested Readings

- [HTML Tables (MDN)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables)
- [Images in HTML (MDN)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Images_in_HTML)
- [Video and Audio Content (MDN)](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)
- [HTML Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference)
