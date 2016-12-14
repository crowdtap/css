# Crowdtap CSS

*A mostly reasonable approach to CSS

## Table of Contents

  1. [Terminology](#terminology)
    - [Rule Declaration](#rule-declaration)
    - [Selectors](#selectors)
    - [Properties](#properties)
  1. [CSS](#css)
    - [Formatting](#formatting)
    - [Comments](#comments)
    - [Colors](#colors)
    - [Quotes](#quotes)
    - [OOCSS and BEM](#oocss-and-bem)
    - [ID Selectors](#id-selectors)
    - [JavaScript hooks](#javascript-hooks)
    - [MediaQueries](#media-queries)

## Terminology

### Rule declaration

A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selectors

In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Properties

Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

## CSS

### Formatting

* Use soft tabs (2 spaces) for indentation
* Prefer dashes over camelCasing in class names.
  - Underscores and PascalCasing are okay if you are using BEM (see [OOCSS and BEM](#oocss-and-bem) below).
* Do not use ID selectors
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations
* Use double quotes consistently. e.g., `content: ""`.

**Bad**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Good**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Comments

* Prefer comments on their own line. Avoid end-of-line comments.
* Write detailed comments for code that isn't self-documenting:
  - Uses of z-index
  - Compatibility or browser-specific hacks

### Colors

When implementing feature styles, you should only be using color variables provided by theme.css

When adding a color variable to theme.css, only use colors available to you by
the color palette. Those should be listed to you in a separate file called
`color_palette.css`.

Using HEX color units is preferred over RGB, RGBA, named, HSL, or HSLA values.

**Good**

```css
#FFF;
#FFFFFF;
```

**Bad**

```css
rgb(50, 50, 50);
white;
hsl(120, 100%, 50%);
hsla(120, 100%, 50%, 1);
```

Using RGBA to set opacity is not a big problem, but has the downside
of using hardcoded color values instead of using the theme variables.

**Not so good**

```css
rgba(50, 50, 50, 0.2);
```

### Quotes

Quotes are optional in CSS and LESS. We use double quotes as it is visually
clearer that the string is not a selector or a style property.

**Good**
```css
background-image: url("/img/you.jpg");
font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial;
```

**Bad**
```css
background-image: url(/img/you.jpg);
font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
```

### OOCSS and BEM

We encourage some combination of OOCSS and BEM for these reasons:

  * It helps create clear, strict relationships between CSS and HTML
  * It helps us create reusable, composable components
  * It allows for less nesting and lower specificity
  * It helps in building scalable stylesheets

**OOCSS**, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusable, repeatable snippets that can be used independently throughout a website.

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki)
  * Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/)

**BEM**, or “Block-Element-Modifier”, is a _naming convention_ for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

We recommend a variant of BEM with camelCased “blocks”.

**Example**

```css
/* listingCard.css */
.listingCard { }
.listingCard--featured { }
.listingCard-title { }
.listingCard-content { }
```

  * `.listingCard` is the “block” and represents the higher-level component
  * `.listingCard-title` is an “element” and represents a descendant of `.listingCard` that helps compose the block as a whole.
  * `.listingCard-featured` is a “modifier” and represents a different state or variation on the `.listingCard` block.

### ID selectors

While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

### JavaScript hooks

Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Media Queries

Place media queries as close to their relevant rule sets whenever possible.
Don't bundle them all in a separate stylesheet or at the end of the document.
Doing so only makes it easier for folks to miss them in the future. Here's a
typical setup.
```css
.element { ... }
.element--selected { ... }
.element-avatar { ... }

@media (min-width: 480px) {
  .element { ...}
  .element--selected { ... }
  .element-avatar { ... }
}
```
