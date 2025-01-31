---
title: ':has()'
slug: Web/CSS/:has
page-type: css-pseudo-class
tags:
  - ':has'
  - CSS
  - Pseudo-class
  - Reference
  - Selector
  - Selectors
browser-compat: css.selectors.has
---

{{CSSRef}}

The functional **`:has()`** CSS [pseudo-class](/en-US/docs/Web/CSS/Pseudo-classes) represents an element if any of the [relative selectors](/en-US/docs/Web/CSS/CSS_Selectors#relative_selector) that are passed as an argument match at least one element when anchored against this element. This pseudo-class presents a way of selecting a parent element or a previous sibling element with respect to a reference element by taking a [forgiving relative selector list](/en-US/docs/Web/CSS/Selector_list#forgiving_relative_selector_list) as an argument.

```css
/* Selects an h1 heading with a
paragraph element that immediately follows
the h1 and applies the style to h1 */
h1:has(+ p) { margin-bottom: 0; }
```

## Syntax

```
:has( <forgiving-relative-selector-list> )
```

The `:has()` pseudo-class cannot be nested within another `:has()`. Also, pseudo-elements are not valid selectors within `:has()`. This is because many pseudo-elements exist conditionally based on the styling of their ancestors and allowing these to be queried by `:has()` can introduce cyclic querying.

The relative selector list is [forgiving](https://drafts.csswg.org/selectors-4/#typedef-forgiving-selector-list). Normally in CSS, when a selector in a selector list is invalid, then the whole list is deemed invalid. When a selector in a `:has()` selector list fails to parse, the incorrect or unsupported selector will be ignored and the others will be used. Note that if the `:has()` pseudo-class itself is not supported in a browser, the entire selector block will fail (unless `:has()` itself is in a forgiving selector list, such as in [`:is()`](/en-US/docs/Web/CSS/:is) and [`:where()`](/en-US/docs/Web/CSS/:where)).

While `:has()` cannot be nested in another `:has()`, as the selector list is forgiving, it will just be ignored. The selector will not fail. The same holds true for pseudo-elements.

## Examples

### With the sibling combinator

The `:has()` style declaration in the following example adjusts the spacing after `H1` headings if they are immediately followed by an `H2` heading.

#### HTML

```html
<section>
  <article>
    <h1>Morning Times</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
  </article>
  <article>
    <h1>Morning Times</h1>
    <h2>Delivering you news every morning</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
  </article>
</section>
```

#### CSS

```css hidden
section {
    display: flex;
    align-items: start;
    justify-content: space-around;
}

article {
  display: inline-block;
  width: 40%;
}

h1, h2 {
  font-size: 1.2em;
}

h2 {
  font-size: 1.0em;
  color: rgb(150, 149, 149);
}
```

```css
h1, h2 {
  margin: 0 0 1.0rem 0;
}

h1:has(+ h2) {
  margin: 0 0 0.25rem 0;
}
```

#### Result

{{EmbedLiveSample('With_the_sibling_combinator', 600, 150)}}

This example shows two similar texts side-by-side for comparison – the left one with an `H1` heading followed by a paragraph and the right one with an `H1` heading followed by an `H2` heading and then a paragraph. In the example on the right, `:has()` helps to select the `H1` element that is immediately followed by an `H2` element (indicated by [`+`](/en-US/docs/Web/CSS/Adjacent_sibling_combinator)) and the CSS rule reduces the spacing after such an `H1` element. Without the `:has()` pseudo-class, you cannot select the preceding sibling or parent element.

### With the :is() pseudo-class

This example builds on the previous example to show how to select multiple elements with `:has()`.

#### HTML

```html
<section>
  <article>
    <h1>Morning Times</h1>
    <h2>Delivering you news every morning</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
  </article>
  <article>
    <h1>Morning Times</h1>
    <h2>Delivering you news every morning</h2>
    <h3>8:00 am</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
  </article>
</section>
```

#### CSS

```css hidden
section {
    display: flex;
    align-items: start;
    justify-content: space-around;
}

article {
  display: inline-block;
  width: 40%;
}

h1 {
  font-size: 1.2em;
}

h2 {
  font-size: 1.0em;
  color: rgb(150, 149, 149);
}

h3 {
  font-size: 0.9em;
  color: darkgrey;
}
```

```css
h1, h2, h3 {
  margin: 0 0 1.0rem 0;
}

:is(h1, h2, h3):has(+ :is(h2, h3, h4)) {
  margin: 0 0 0.25rem 0;
}
```

#### Result

{{EmbedLiveSample('With_the_:is()_pseudo-class', 600, 170)}}

Here, the first [`:is()`](/en-US/docs/Web/CSS/:is) pseudo-class is used to select any of the heading elements in the list. The second `:is()` pseudo-class is used to pass a selector list as an argument to `:has()`. The `:has()` pseudo-class helps to select any `H1`, `H2`, or `H3` element that is immediately followed by (indicated by [`+`](/en-US/docs/Web/CSS/Adjacent_sibling_combinator)) an `H2`, `H3`, or `H4` element and the CSS rule reduces the spacing after such `H1`, `H2`, or `H3` elements.

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [`:is()`](/en-US/docs/Web/CSS/:is), [`:not()`](/en-US/docs/Web/CSS/:not)
- [CSS selectors](/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS combinators](/en-US/docs/Learn/CSS/Building_blocks/Selectors/Combinators)
- [Selector list](/en-US/docs/Web/CSS/Selector_list)
- [Locating DOM elements using selectors](/en-US/docs/Web/API/Document_object_model/Locating_DOM_elements_using_selectors)
