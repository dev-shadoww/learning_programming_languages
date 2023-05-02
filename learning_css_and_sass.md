# Learning CSS

## Introduction to Sass

`Sass` is a `css` preprocessor, an extension of css, the styles is written in `sass` files which is then compiled to `css` through a `sass` compiler.

### Variables in Sass

```css
$color-black: #000;
$color-white: #fff;

ul {
  color: $color-black;
}
```

### Nesting in Sass

```html
<ul>
  <li></li>
  <li>b</li>
</ul>
```

```css
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

```css
@mixin turnColor {
  color: blue;
}

header {
  @include turnColor;
}
```

Passing arguments to `mixins`,

```css
@mixin turnColor($color) {
  color: $color;
}
```

### Functions

```css
@function divide($a, $b) {
  @return $a / $b;
}
```

### Extends

```css
%turnColor {
  color: blue;
}

ul {
  @extend turnColor;
}
```
