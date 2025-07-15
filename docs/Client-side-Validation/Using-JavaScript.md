---
id: Using-JavaScript
title: Using JavaScript
sidebar_position: 2
description: Using JavaScript
---

# Using JavaScript

## JavaScript and Client-Side Validation

All of the methods above are examples of static checks (i.e., they don't change)
that we're adding to our form controls. They do a lot to help guard against
invalid data; however, there are times that we need more flexible control
over what happens.

In order to add dynamic checks (i.e., can be changed at runtime) we need to layer
in use of JavaScript. By using JavaScript we have more freedom to create custom
and complex validation rules beyond the set of static options provided by HTML
and the browser. We can also use JavaScript in combination with CSS to provide
a better user experience:

- display more meaningful, context-aware error messages
- show/hide error messages depending on the location of the cursor and where the user is focused
- place errors (or other information) anywhere in the DOM vs. being limited to labels, placeholder or tooltip text

### Accessing Form Fields

When writing JavaScript to validate form fields, there are a number of ways
to access the input controls and get their values. Consider the following
form:

```html
<form id="info-form" name="info" action="/i">
  <input id="first-name" name="fname" type="text" />
  <input id="number-list" name="number-list" type="text" />
</form>
```

Here are some of different ways we could access this form:

```js
// 1. Using its id and getElementById()
var form = document.getElementById('info-form');

// 2. Using its id and querySelector()
var form = document.querySelector('#info-form');

// 3. Using document.forms and the id or name of the form
var form = document.forms['info-form'];
```

Once we have a reference to the `<form>` element in JavaScript, we can use the
`name` of the form controls to get access to the individual fields and there `.value`:

```js
// Notice that we must wrap values with '-' in their names in ["..."] to access them.
var form = document.forms['info-form'];
var fname = form.fname.value;
var numberList = form['number-list'].value;
```

### Special Cases for Obtaining Form Values

Some form controls need different approaches when you want to access their value
in JavaScript:

1. `<textarea>`: use the `.value` property to access the text.
1. `<input type="radio">`: use the `name` property (i.e., all radio buttons will use the same `name` in a group) to iterate over all possible radio controls, and then look at the `.checked` property, which will be `true` for the one checked.
1. `<input type="checkbox">`: use the `name` property to iterate over all possible radio controls, and then look at the `.checked` property, which will be `true` for the one checked.
1. `<select>`: use the `selectedIndex` to determine which `<option>` index was selected (if any). A value of `-1` means none are currently selected; a value greater than `-1` indicates the index to use when accessing the `options[n]` array for the chosen option. If the `<select>` is defined to allow for `multiple` options, you can loop through the options and inspect the `.selected` property to determine if it's `true`.

Consider the following form:

```html
<form id="info-form" name="info" action="/i">
  <label for="text">Enter some text</label>
  <textarea id="text" name="text"></textarea>

  <fieldset>
    <legend>Pick a Colour</legend>

    <label for="colour-red">Red</label>
    <input type="radio" name="colour" id="colour-red" value="red" checked />

    <label for="colour-green">Green</label>
    <input type="radio" name="colour" id="colour-green" value="green" />

    <label for="colour-blue">Red</label>
    <input type="radio" name="colour" id="colour-blue" value="blue" />
  </fieldset>

  <label for="agree-disagree">I agree with the terms and conditions.</label>
  <input type="checkbox" name="agree" id="agree-disagree" />

  <label for="food">Favourite Food</label>
  <select id="food" name="food">
    <option value="pizza">Pizza</option>
    <option value="tacos">Tacos</option>
    <option value="salad">Salad</option>
    <option value="other">Other</option>
  </select>
</form>
```

In order to access the form's values in code, we could do the following:

```js
var form = document.querySelector('#info-form');

// Get the value form the <textarea>
var text = form.text.value.trim();

// Get the chosen colour value from the radio button group
var colour;
var colourChoices = Array.from(form.colour); // convert to array
colourChoices.forEach(function (option) {
  if (option.checked) {
    colour = option.value;
  }
});

// Get the chosen food value form the <select>
var food = 'None'; // there may be nothing selected
var foodChoices = Array.from(form.food); // convert to array
foodChoices.forEach(function (option) {
  if (option.selected) {
    food = option.value;
  }
});
```

### Using the `submit` Event to Validate Forms with JavaScript

There are a wide variety of custom validation tests we can write via JavaScript:

- Check for the presence or absence of a field
- Check the value of a field, and determine if it's within an expected range, of a specific type, etc.
- Confirm that some value is "real" vs. matching an expected format. (e.g., does a user id exist?)
- Evaluate a group of input values together as a group. Do they make sense together?

An HTML `<form>` element exposes the `submit` event (and `onsubmit` event property), which
we can use to add custom JavaScript code to handle the case that the user is trying to
submit a form:

```html
<form id="info-form" name="info" action="/i">...</form>
<script>
  var infoForm = document.getElementById('info-form');

  // submit event fired when the user clicks "submit" button
  infoForm.onsubmit = function () {
    // Perform extra validation here.  When finished validating, return
    // either `true` (form is valid) or `false` (form is invalid) to tell
    // the browser how to proceed.
  };

  // reset event fired when the user clicks a "reset" button
  infoForm.onreset = function () {
    // If you ever need to do extra work to clear a form, do it here.
  };
</script>
```

Consider the example of a form that asks the user to enter a list of 2-4
numbers. We'd like to allow the user as much freedom to enter this list as possible,
and support any style of entry:

```html
<div id="error-msg" class="error hidden"></div>

<form id="info-form" name="info" action="/i">
  <label for="number-list">Number list</label>
  <input id="number-list" name="list" type="text" />
</form>
<script>
  var infoForm = document.getElementById('info-form');

  infoForm.onsubmit = function () {
    // Check if number list is valid, and return true if it is
    if (validateNumberList()) {
      // Hide the error message if it was displayed previously
      hideErrorMessage();
      return true;
    }

    // Number list is invalid, so display error message and return false
    showErrorMessage('Number list is invalid: expected 2 to 4 numbers in a list.');
    return false;
  };

  function showErrorMessage(msg) {
    var errMessage = document.querySelector('#error-msg');
    // Remove the hidden class so the error message shows.
    errMessage.classList.remove('hidden');
    // Set the error message text
    errMessage.innerHTML = msg;
  }

  function hideErrorMessage(msg) {
    var errMessage = document.querySelector('#error-msg');
    // Add the hidden class so the error message goes away.
    errMessage.classList.add('hidden');
  }

  function getNumberList() {
    // Get the number-list <input> value
    var list = document.querySelector('#number-list').value;

    // Get rid of leading/trailing spaces
    list = list.trim();

    // Split the string into an array, separated by spaces, commas, or a combo of each
    return list.split(/[ ,]+/);
  }

  function validateNumberList() {
    var list = getNumberList();

    // Make sure we have between 2 and 4 elements.  If not, return `false`
    // to indicate this form is invalid (don't submit)
    if (!(list.length >= 2 && list.length <= 4)) {
      return false;
    }

    // Make sure each element in the list is a number
    function isNumber(n) {
      return !isNaN(n);
    }

    // Loop across every value in the array, and call isNumber() on the value.
    // Return true if EVERY element passes isNumber, and false otherwise.
    return list.every(isNumber);
  }
</script>
```
