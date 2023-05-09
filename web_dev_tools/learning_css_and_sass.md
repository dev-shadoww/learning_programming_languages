# Learning CSS

## CSS Properties

`Global Reset`,

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.7;
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
