# Learning CSS

## CSS Properties

`Global Reset`,

```css
* {
  margin: 0;
  padding: 0;
}

*,
*::before,
*::after {
  box-sizing: inherit;
}

html {
  box-sizing: border-box;
  font-size: 62.5%;
}

body {
  font-family: sans-serif;
  font-weight: 400;
  color: #777;
}
```

`clip-path: polygon()` it takes 4 parameters, which are the position x and y,

```css
header {
  clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
}
```

Centering elements with absolute positing,

```css
div {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(50%, 50%);
}
```

Animations,

```css
.box {
  animation-name: AnimationAtStart;
  animation-duration: 5s;
  animation-delay: 3s;
  animation-iteration-count: 3;
  animation-timing-function: ease-out;
}

@keyframes AnimationAtStart {
  0% {
    opacity: 0;
    transform: translateX(-100px);
  }

  100% {
    opacity: 1;
    transform: translateX(0px);
  }
}
```

Styling a button,

```css
.btn:link,
.btn:visited {
  text-transform: upperCase;
  text-decoration: none;
  padding: 15px 40px;
  display: inline-block;
  border-radius: 100%;
  transition: all 0.2s;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  position: relative;
}

.btn::after {
  content: "";
  display: inline-block;
  height: 100%;
  width: 100%;
  border-radius: 100px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
}

.btn:hover::after {
  transform: scale(1.2);
}
```

Text coloring,

```css
.heading {
  background-image: linear-gradient(to bottom right, #000, #fff);
  -webkit-background-clip: text;
  color: transparent;
}
```

## CSS FlexBox

`FlexBoxes` are used to create 2-dimensional layouts,

```html
<div class="flex-container">
  <p class="flex-item">Flex Item</p>
</div>
```

```css
.flex-container {
  display: flex;
}
```

`Flex Container` properties,

- `flex-direction: row | row-reverse | column | column-reverse`
- `flex-wrap: nowrap | wrap-reverse`
- `justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly`
- `align-items: stretch | flex-start| flex-end| center| baseline`
- `align-content: stretch | flex-start | flex-end | center | space-between | space-around`

`Flex Item` properties,

- `align-self: auto | stretch | flex-start | flex-end | center | baseline`
- `order: 0 | <integer>`
- `flex-grow: 0 | <integer>`
- `flex-shrink: 1 | <integer>`
- `flex-basis: auto | <length>`

## CSS Grids

```html
<div class="grid-container">
  <p class="grid-item">Grid Item</p>
</div>
```

```css
.flex-container {
  display: grid;
}
```

`Grid Container` properties,

- `grid-template-rows, grid-template-columns, grid-template-areas`
- `grid-row-gap, grid-column-gap`
- `justify-items, align-items, justify-content, align-content`
- `grid-auto-rows, grid-auto-columns, grid-auto-flow`

`Grid Items` properties,

- `grid-row-start, grid-row-end, grid-column-start, grid-column-end`
- `justify-self, align-self`
- `order`

## Writing media queries using sass

Here `1em = 16px`,

```scss
@mixin respond($breakPoint) {
  @if $breakPoint == phone {
    @media (max-width: 37.5em) {
      @content;
    }
  }

  @if $breakPoint == tab-port {
    @media (max-width: 56.25em) {
      @content;
    }
  }

  @if $breakPoint == tab-land {
    @media (max-width: 75em) {
      @content;
    }
  }

  @if $breakPoint == big-desktop {
    @media (max-width: 112.5em) {
      @content;
    }
  }
}
```

## Responsive images

### Resolution switching

Decrease image resolution on smaller screens.

```html
<img
  srcset="image-1x.png 200w, image-2x.png 300w"
  sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
/>
```

### Density Switching

Half the resolution.

```html
<img srcset="image-1x.png 1x, image-2x.png 2x" />
```

### Art Direction

Different image on smaller screens.

```html
<picture>
  <source
    srcset="image-1x.png 1x, image-2x.png 2x"
    media="(max-width: 37.5em)"
  />
</picture>
```

## Testing for browser support

```css
@supports (backdrop-filter: blur(20px)) {
  backdrop-filter: blur(20px);
}
```

## Introduction to Sass

`Sass` is a `css` preprocessor, an extension of css, the styles is written in `sass` files which is then compiled to `css` through a `sass` compiler.

### Variables in Sass

In `sass` variables are written in the form `$variable-name: value;`.

```scss
$color-black: #000;
$color-white: #fff;

ul {
  color: $color-black;
}
```

### Nesting in Sass

`Sass` provides nesting, the `&` represents the parent class in nesting.

```html
<ul>
  <li></li>
  <li>b</li>
</ul>
```

```scss
ul {
  font-size: 10px;
  li {
    background-color: #000;

    &:first-child {
      color: red;
    }
  }
}
```

Here, `&` is converted into the parent selector(element).

### Mixins

```scss
@mixin turnColor {
  color: blue;
}

header {
  @include turnColor;
}
```

Passing arguments to `mixins`,

```scss
@mixin turnColor($color) {
  color: $color;
}
```

### Functions

```scss
@function divide($a, $b) {
  @return $a / $b;
}
```

### Extends

```scss
%turnColor {
  color: blue;
}

ul {
  @extend turnColor;
}
```

### Building Grid Layout

```scss
.row {
  max-width: 114rem;
  margin: 0 auto;

  &:after {
    content: "";
    display: table;
    clear: both;
  }

  [class^="col"] {
    float: left;

    &:not(:last-child) {
      margin-right: 6rem;
    }
  }

  &:not(:last-child) {
    margin-bottom: 8rem;
  }

  .col-1-of-2 {
    width: calc((100% - 8rem) / 2);
  }

  .col-1-of-3 {
    width: calc((100% - 8rem) / 3);
  }
}
```
