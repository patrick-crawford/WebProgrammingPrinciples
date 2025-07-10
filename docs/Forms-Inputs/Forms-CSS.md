---
id: Forms-CSS
title: Forms & CSS
sidebar_position: 2
description: Forms & CSS
---

# Forms & CSS

HTML forms have evolved and improved significantly in HTML5 and modern browsers.
As you learn how to create and style your own forms, be aware that many resources
give outdated advice, or use unnecessary workarounds and tricks to create functionality
that is now built into the web.

Form controls use the CSS box model, but [each one applies it slightly differently](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Styling_HTML_forms#Box_model).
This can make it hard to align everything. We can make things easier by altering
our controls' [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) to use [`border-box`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing#Values), where the `width` and `height` also include the controls content, padding, and border. This
helps to even out the inconsistencies between different controls and their sizes:

```css
/* Example: make all controls 150px wide */
input,
textarea,
select,
button {
  width: 150px;
  margin: 0;
  box-sizing: border-box;
}
```

When working with `<label>`s and `<span>`s in forms, it's common to need to specify
their width and height, so that they properly align with other controls in the form. By default these controls are displayed as `inline` elements, but we can instead use
[`display: inline-block;`](http://learnlayout.com/inline-block.html) to add a `width`
and `height` to an inline element.

```css
label {
  display: inline-block;
  width: 100px;
  text-align: right;
}
```

## CSS Selectors and Forms

There are a number of CSS selectors that are useful when working with forms.

An attribute selector allows us to match on the basis of either:

- the presence of an attribute
- the exact or partial match of an attribute's value

For example, consider the following:

```css
/* Style submit input controls */
input[type='submit'] {
  border: 2px solid #ccc;
}
```

Another useful selector type are the various sibling selectors:

```css
/* Style all <input> elements that are direct siblings of a <label> */
label+input {
    ...
}

/* Style all <input> elements that are siblings (direct or indirect) of a <label> */
label~input {
    ...
}
```

Finally, a range of pseudo-selectors can be added to other elements/selectors
to specify the state of a form control:

- `:valid` - style to be used when the value meets all of the validation requirements.
- `:invalid` - style to be used when the value does not meet all of the validation requirements.
- `:required` - style for an input element that has the required attribute set.
- `:optional` - style for an input element that does not have the required attribute set.
- `:in-range` - style for a number input element where the value is in range.
- `:out-of-range` - style for a number input element where the value is out of range.

## Suggested Readings

- [HTML Forms](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms)
- [Designing Efficient Web Forms: On Structure, Inputs, Labels and Actions](https://www.smashingmagazine.com/2017/06/designing-efficient-web-forms/)
- [Create Amazing Forms](https://developers.google.com/web/fundamentals/design-and-ux/input/forms/)
- [Bootstrap Forms](https://getbootstrap.com/docs/4.1/components/forms/)
