# Learning CSS

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

## CSS Properties
