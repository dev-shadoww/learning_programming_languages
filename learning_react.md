# Learning React

## Introduction

```javascript
/*
  1) Import REACT and REACTDOM

  React knows how to work with components, ReactDOM knows how to render it on screen.
*/

import React from "react";
import ReactDOM from "react-dom/client";

/* 
  2) Get reference to the div with id root
*/

const el = document.getElementById("root");

/* 
  3) Tell react to take control of that element
*/

const root = ReactDOM.createRoot(el);

/* 
  4) Create a component
*/

function App() {
  return <h1>Hello World !</h1>;
}

/* 
  5) Show the component on screen
*/

root.render(<App />);
```

Here the `<h1>Hello World !</h1>` is called as `JSX`, `JSX` stands for `JavaScript XML`. `JSX` allows us to write HTML in React. `JSX` makes it easier to write and add HTML in React.

### Passing variable in `JSX`

```javascript
function App() {
  const text = "Hello World !";

  return <h1>{text}</h1>;
}
```

### Customizing elements with props

```javascript
function App() {
  return <input type="number" min={5} />;
}
```

For `props`, wrap `strings` with double quotes, and wrap `numbers` with curly braces and wrap `arrays`, `objects` and `variables` in curly braces.

We can provide `object` as props values, but not to display them.

### Converting HTML to JSX

- All props name follow `camelCase`
- `Number` attributes use curly braces
- Boolean `true` can be written with just the property name, `False` should be written in curly braces
- The class attribute is written as `className`
- `Inline styles` are provided as objects

## Building with reusable components

### Props System

The `Props System` allows us to pass data from parent to child component. It is one way flow of data.

- Add attributes to `JSX` elements
- React collects them and puts them into a object
- Then this object shows up as first argument to child component
- Now the props can be used in child component

`App.js`

```javascript
function App(){
  return <Diff use="test_example">
}
```

`diff.js`

```javascript
function Diff(props) {
  return <div>{props.use}</div>;
}
```
