# Learning React

## Introduction

```javascript
import React from "react";
import ReactDOM from "react-dom/client";

const el = document.getElementById("root");

const root = ReactDOM.createRoot(el);

function App() {
  return <h1>Hello World !</h1>;
}

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
- Don't call it, instead just pass it as reference
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

Whenever the state changes, react rerenders the page automatically.

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

`App.js`

```javascript
import AppComponent from "./AppComponent";

function App() {
  const handleSubmit = (term) => {
    console.log(term);
  };

  return (
    <div>
      <AppComponent onSubmit={handleSubmit} />
    </div>
  );
}

export default App;
```

`AppComponent.js`

```javascript
function AppComponent({onSubmit}){
  function handleClick(){
    onSubmit();
  }

  return (
    <div>
      <button onClick={handleClick}><button/>
    </div>;
  )
}

export default AppComponent;
```

### Working with forms

Here html `forms` are used to handle both `enter` and `click` events, but the from in browser by default tries to make contact with website, so to prevent it we use `event.preventDefault()`.

Handling text inputs,

- Create new piece of data
- Create a eventHandler to watch for `onChange` event
- When it fires, get the value from the input
- Take this value to update the state
- Pass the state to the input as prop value

```javascript

import {useState} from 'react';

function AppComponent({onSubmit}){
  const [term, setTerm] = useState('');

  function handleFormSubmit(event){
    event.preventDefault();
    onSubmit();
  }

  function handleChange(event){
    setTerm(event.target.value)
  }

  return (
    <div>
      <form onSubmit={handleFormSubmit}>
        <input value={term} onChange={handleChange}/>
      </form>
    </div>;
  )
}

export default AppComponent;
```

Handling list updates,

- Apply a `key` to each element during mapping step
- After re-rendering compare keys on each value to the keys from previous render
- Apply minimal set of changes to existing HTML

Requirement of `keys`,

- Use, if there is a list of elements
- Add key to the topmost `jsx` element
- Must be a string or number
- Should be unique for the list
- Should be consistent across the rerenders

## Handling forms

Updating a state with respect to array and objects,

```javascript
const handleCreate = (item) => {
  const [items, setItems] = useState([]);

  const itemsList = [...items, item];

  setItems(itemList);
};
```

Inserting using `slice()`,

```javascript
const handleCreate = (item, index) => {
  const [items, setItems] = useState([]);

  const itemsList = [...items.slice(0, index), item, items.slice(index)];

  setItems(itemList);
};
```

Removing elements using `filter()`,

```javascript
const handleCreate = (item) => {
  const [items, setItems] = useState([]);

  const removeItems = (removeItem) => {
    const itemsList = items.filter((item) => item != removeItem);
    setItems(itemList);
  };
};
```

Adding or changing properties in objects,

```javascript
const handleCreate = () => {
  const [items, setItems] = useState({
    color: red,
  });

  const changeValue = (color) => {
    const updatedItems = { ...items, color: color };

    setItems(updatedItems);
  };

  const removeValue = (color) => {
    const { color, ...rest } = items;

    setItems(rest);
  };
};
```

`useEffect` is used to run code when a component is initially rendered, or it is rerendered.

```javascript
import { useEffect } from "react";

useEffect(() => {
  console.log("hello React");
}, []);
```

The code runs based on the second argument, in this case when the array is empty then it is called.

## Communication using the context system

Context system is alternate to props.

Using Context,

- Create Context, it provides a `provider` (component used to specify what data we want to share) and `consumer` (Component used to get access to data).

```javascript
import { createContext } from "react";

const ExampleContext = createContext();

export default ExampleContext;
```

- Specify data that will be shared

Here `<MyContainer>` and it's children can get the value,

```javascript
<ExampleContext.Provider value={5}>
  <MyContainer>
</ExampleContext.Provider>
```

- Consume the data in component

```javascript
import { useContext } from "react";
import ExampleContext from "./Example";

function myComponent() {
  const num = useContext(ExampleContext);

  return <div>num</div>;
}
```

### Changing Context Values

```js
import { createContext, useState } from 'react';

const ExampleContext = createContext();

function Provider({children}){
  const [count, setCount] - useState(0);

  const valueToShare = {
    count: count,
    incrementCount: () => {
      setCount(count + 1);
    }
  };

  return(
    <BooksContext.Provider value={valueToShare}>
        {children}
    <BooksContext.Provider>
  )
}
```

### Application State, Component State

In Application State data is used by many different applications, but in Component State data is used by very few components.

Share all the states in Application State with `Context System`.

## Hooks

Hooks are functions that add additional functionality to the components.

### useCallback

The `useEffect` has a major bug which makes some of the applications behave abnormally, so to avoid that `useCallback` is used.

```js
const stableExample = useCallback(exampleFunction(), []);
```

It returns the function which is passed as first argument, as in `useEffect` creates separate variables with the same name, and it causes the abnormal behavior of the `useEffect`.

```js
useEffect(() => {
  stableExample();
}, [stableExample]);
```

The `useEffect` can only return functions and nothing else.

```js
useEffect(() => {
  const greet = () => {
    console.log("Hello from useEffect");
  };

  return greet;
}, []);
```

Here the `greet` is called from second render onwards, on first render useEffect returns the function and holds a reference to it, on the second render it calls the function, and create a new function and returns it.

## React Navigation

Anything that is placed between component tags will be passed as prop with tag `children`.

```js
function App() {
  return (
    <div>
      <Button>Text Is Passed!!</Button>
    </div>
  );
}
```

```js
function Button({ children }) {
  return <button>{children}</button>;
}

export default Button;
```
