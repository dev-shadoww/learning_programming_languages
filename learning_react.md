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

### Event System and State System

To use `Event System`,

- Decide the type of event
- Write a function with the name following pattern `handle + EventName`
- Pass the function as prop
- Then don't call it, instead just pass it as reference
- Pass it using a valid event name, like `onClick`, `onMouseOver` etcetera.

```javascript
function App() {
  const handleClick = function () {
    console.log("Button was clicked");
  };

  return <div onClick={handleClick}>Button</div>;
}
```

Two most common events, `onClick`, `onChange`.

To use `State System`,

`State` is data that changes as the user interacts with the app, when this data changes the react will update it automatically.

```javascript
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  const handleClick = function () {
    setCount(count + 1);
  };

  return (
    <div>
      <button onClick={handleClick}>Click here</button>
      <div>The count is : {count}</div>
    </div>
  );
}
```

- Import `useState` from `react`
- `const [count, setCount] = useState(0)`, here `[count, setCount]` is the array destructuring, `useState(0)` is the default value for this state, `count` piece of state, `setCount` used to update the piece of state.

## Using an API in react

`React` doesn't have any inbuilt functionalities to work with API's, for this we need to use 3rd party libraries (like `axios`) or javascript's `fetch()` API,

### Communication from child to parent

In `React` siblings can't communicate directly, they need to communicate through the parent.
