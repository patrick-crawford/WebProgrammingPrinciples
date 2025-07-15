---
id: Data-Formats
title: Data Formats
sidebar_position: 2
description: Data Formats
---

# Data Formats

## Working with Data: JSON and XML

Our previous example used a very simple data format: a single number. Often
we'll need to work with more complex data, which includes both numbers and text,
lists, and complex hierarchies. To do this, we need a format that allows us
to serialize (i.e., turn into strings) data structures like `Array`s, `Object`s, etc.

The two most popular formats for data exchange on the internet are the
[JavaScript Object Notation (JSON)](https://en.wikipedia.org/wiki/JSON) and the
[Extensible Markup Language (XML)](https://en.wikipedia.org/wiki/XML).

We're going to focus mainly on JSON, but it's good to also know about XML. At
one point, a lot of the techniques we will discuss were done with XML (and many
languages and services still use it). However, much of the internet has
standardized on JSON as a data exchange format.

Let's look at each in turn. First, consider the following food product data:

```
1) Name: Apple
   Price per Pound: $1.29
   Location: Aisle 3

2) Name: Carrots
   Price per Pound: $0.46
   Location: Aisle 2
```

Here's how that data might look using XML:

```xml
<products>
    <product>
        <name>Apple</name>
        <price currency="CAD">1.29</price>
        <aisle>3</aisle>
    </product>
    <product>
        <name>Carrots</name>
        <price currency="CAD">0.46</price>
        <aisle>2</aisle>
    </product>
</products>
```

Look familiar? XML and HTML are both markup languages. In XML, it's
possible for us to create our own tags and document structure (i.e., XML Schema).
You can think of HTML like an instance of XML, which is what [XHTML](https://en.wikipedia.org/wiki/XHTML) was trying to do.

Before we look at JSON, let's look at that same data in JavaScript, using an Object Literal:

```js
var products = [
  {
    name: 'Apple',
    price: {
      currency: 'CAD',
      value: 1.29,
    },
    aisle: 3,
  },
  {
    name: 'Carrots',
    price: {
      currency: 'CAD',
      value: 0.46,
    },
    aisle: 2,
  },
];
```

Here we have two `Object`s in an `Array`. Our `Object`s use `String`, `Object`,
and `Number` types to represent the data.

Finally, let's format the same data in JSON:

```json
[
  {
    "name": "Apple",
    "price": {
      "currency": "CAD",
      "value": 1.29
    },
    "aisle": 3
  },
  {
    "name": "Carrots",
    "price": {
      "currency": "CAD",
      "value": 0.46
    },
    "aisle": 2
  }
]
```

Looks familiar, doesn't it? You'll be glad to know that since you
already learned JavaScript Object Literals, you already learned 95% of JSON format at the same time.

JSON and JavaScript Object Literals are very similar, but there are some
differences. JSON is a subset of JavaScript Object Literal notation:

- All keys must be double-quoted strings: `"key"` vs. `key`
- You don't put comments in JSON
- You can't include function expressions in JSON, only data types:
  - `String`
  - `Number`
  - an (JSON) `Object`
  - an `Array`
  - boolean `true` or `false`
  - the value `null`

JavaScript includes built-in code for converting to/from JSON strings:

```js
var products = [
  {
    name: 'Apple',
    price: {
      currency: 'CAD',
      value: 1.29,
    },
    aisle: 3,
  },
  {
    name: 'Carrots',
    price: {
      currency: 'CAD',
      value: 0.46,
    },
    aisle: 2,
  },
];
// 1. Turn products Object into JSON string
var json = JSON.stringify(products);
// json now equals '[{"name":"Apple","price":{"currency":"CAD","value":1.29},"aisle":3},{"name":"Carrots","price":{"currency":"CAD","value":0.46},"aisle":2}]'

// 2. Turn JSON string back into a JS Object
products = JSON.parse(json);
// products is now an Object
```

> NOTE: `JSON.parse()` will `throw` an error if the string isn't properly formatted JSON, so it's good to wrap your call in a `try...catch` block.

## Example 2: the Dog API

For our next example, let's work with another web service, but this time
one that returns more complex data in the form of JSON.

The [Dog API](https://dog.ceo/dog-api/documentation/) is a free web service
that uses data from the [Stanford Dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/). This dataset contains
images and information about 120 breeds of dogs, and is used for machine learning
and artificial intelligence training.

There are a number of endpoints we can use with this API, but we'll focus on these:

- [https://dog.ceo/api/breeds/list/all](https://dog.ceo/api/breeds/list/all) - get a JSON formatted list of all breeds and sub-breeds
- [https://dog.ceo/api/breed/hound/images/random/3](https://dog.ceo/api/breed/hound/images/random/3) - get a JSON formatted list of image URLs for hounds, returning 3 (we can ask for more or less) In other words the URL works like this: `https://dog.ceo/api/breed/{name-of-breed}/random/{number-of-images-to-return}`

Our goal is to do the following:

1. Create a simple web page with an HTML `<form>`
1. Use AJAX techniques to dynamically load all dog breeds into a `<select>` in our form
1. Users can specify how many images they want to load: 1 to 100.
1. When the user selects a breed and clicks a `<button>`, we'll request the JSON list of images
1. Once we get the list of image URLs, we'll start creating `<img>` elements in our page to show those dogs

See the completed code in [dogs.zip](files/dogs.zip).
We'll discuss snippets of the code below.

### 1. Create a form

Let's start with a basic `<form>`:

```html
<form id="dogs-form" action="#">
  <select id="breeds" name="breeds"></select>
  <input type="number" min="1" max="100" value="5" />
  <input type="button" id="btn-load" value="Show me dogs!" />
</form>
```

Our form is very simple. Notice that it contains no `<option>` elements
for the dog breeds. We will load these dynamically once the page is loaded.
We include a textbox for entering a number of images to show (default is `5`),
and provide a `<button>` to click.

### 2. Dynamically load dog breeds into a drop-down

Next we need to load our dog breeds from the Dogs API. We'll do that
when the page finishes loading, and the DOM is fully created:

```js
window.onload = function () {
  loadDogBreeds();
};
```

Our `loadDogBreeds` function needs to create an XHR request to the Dogs API,
and parse the JSON we get back:

```js
function loadDogBreeds() {
  // See https://dog.ceo/dog-api/documentation/
  var url = 'https://dog.ceo/api/breeds/list/all';
  var xhr = new XMLHttpRequest();

  xhr.onload = function () {
    var response = JSON.parse(this.responseText);
    var breedList = extractBreedList(response);
    updateBreedList(breedList);
  };
  xhr.open('GET', url);
  xhr.send();
}
```

When our request comes back (i.e., `xhr.onload`), we'll get a JSON string
that looks something like this:

```
"{"status":"success","message":{"affenpinscher":[],"african":[],"airedale":[],"akita":[],"appenzeller":[]}}";
```

If we `JSON.parse()` that string, we'll get an `Object` that looks like this:

```js
var response = JSON.parse(this.responseText);
/*
{
    status: "success",
    message: {
        affenpinscher: [],
        african: [],
        airedale: [],
        akita: [],
        appenzeller: [],
        ...
    }
}
*/
```

This data has two main parts:

1. a `status` message, that tells us the server was successful in doing our query
1. a `message` body, which is itself an `Object` of key/value pairs, with the breed name and sub-breeds (if any) in an `Array`.

To get all the dog breeds as a list (i.e. `Array`), we need to extract the
`message` property, then call [`Object.keys()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
on its value to create an `Array` out of all the names:

```js
var breedList = Object.keys(response);
/*
['affenpinscher', 'african', 'airedale', 'akita', 'appenzeller', ...]
*/
```

Next we need to take this list of breed name `String`s, and create
`<option>` elements that we can dynamically add to our form's `<select>`:

```js
// Get a reference to our <select>
var select = document.querySelector('#breeds');

// Given a breed name "beagle", return an <option value="beagle>beagle</option>
function createBreedOption(name) {
  var option = document.createElement('option');
  option.value = name;
  option.innerHTML = name;

  return option;
}

// Loop through each breed name in our Array, call createBreedOption()
// and append the <option> element to our <select>
breedList.forEach(function (breed) {
  var breedOption = createBreedOption(breed);
  select.appendChild(breedOption);
});
```

Our web page now has a drop-down list with all 120 dog breeds.

### 3. Get dog breed image URLs when the user selects a breed

When the user selects a breed from our list and clicks a `<button>`,
we need to make another HTTP request to the server. This time
we need to get a list of image URLs for the chosen breed.

First, we need an event handler for the click:

```js
var btnLoad = document.querySelector('#btn-load');

btnLoad.onclick = function (e) {
  var breed = document.querySelector('#breeds').value;
  loadBreedImages(breed);
};
```

Our `loadBreedImages` function is nearly identical to `loadDogBreeds`, but
we use the `breed` name as part of the URL:

```js
function loadBreedImages(breed) {
  // See https://dog.ceo/dog-api/documentation/breed
  // Use the imageCount and breed variables to create our URL
  var imageCount = document.querySelector('#image-count').value;
  var url = `https://dog.ceo/api/breed/${breed}/images/random/${imageCount}`;
  var xhr = new XMLHttpRequest();

  xhr.onload = function () {
    try {
      var response = JSON.parse(this.responseText);
      var breedImageList = extractBreedImageList(response);
      updateBreedImages(breedImageList);
    } catch (e) {
      showError('Unable to load dog breeds');
    }
  };

  xhr.open('GET', url);
  xhr.send();
}
```

As before, we make a request to the server, and get back JSON, which we
parse. The resulting `Object` we get back looks like this:

```js
{
    status: "success",
    message: [
       "https://images.dog.ceo/breeds/hound-afghan/n02088094_1003.jpg",
       "https://images.dog.ceo/breeds/hound-afghan/n02088094_1007.jpg",
       ...
    ]
}
```

Once again we get a `status` and a `message` body. This time, however,
the `message` is already an `Array` of URLs.

### 4. Dynamically create &lt;img&gt; elements for all dog breed image URLs

Using the list of URLs for dog breed images from the server, we can
easily update our page to display new images:

```js
var imagesContainer = document.querySelector('#images-container');

// Clear the imagesContainer if there is anything there now
imagesContainer.innerHTML = '';

// Turn a url String into an <img src="url"> element
function createImgElement(url) {
  var img = document.createElement('img');
  img.src = url;
  return img;
}

// Loop through the image URLs, and create new <img> elements
breedImageList.forEach(function (url) {
  var img = createImgElement(url);
  imagesContainer.appendChild(img);
});
```

We've now got a relatively simple page that can be changed using live data
to look completely different, depending on the needs of the user. We didn't
have to write HTML for every image, which would have involved hand-writing
120 \* 150 = 18,000 `<img>` elements! Using AJAX we can do this with very
little code.

Complete code for the example above can be found in the following file: [dogs.zip](files/dogs.zip).
