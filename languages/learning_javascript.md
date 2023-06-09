# Learning JavaScript

## Fundamentals

Before writing enable strict mode by `use strict`,

### `console.log()`

It prints the value to the console,other methods on `console` are,

`console.table()`, `console.dir()`, `console.error()`

### Variables and Data Types

In `JS` we can define variable in 3 ways, using `let`, `const` and `var`.

`let`, Can change the value, creates a block scope, `const`, Cannot change the value, creates a scope, `var` Don't use it, doesn't create a function scope,

```javascript
let user = root;

const fruit = apple;

var vehicle = bike;
```

In `JS` the available data types are, `Numbers`, `Booleans`, `Strings`, `Undefined`, `Null`, `Symbol` and `Bigint`, and it has dynamic typing.

`typeof` can be used to check the type of a variable,

```javascript
let example = 23;
let userName = "root";
let isNumber = true;
let logged = undefined;
```

The `0`, `''`, `undefined`, `null`, `Nan` are `falsy` values.

`Template Literals`,

```javascript
console.log(`The example value is ${example}.`);
```

In javascript `+` converts numbers into strings and `-` operator converts strings into numbers.

### Numbers

`+` converts, `'23'` to 23,

```javascript
console.log(+"23");

Number.parseInt("23x");
Number.parseFloat("2.3x");
Number.isNan(20);
Number.isFinite(20);
Number.isInteger(20);

console.log((23).toFixed(2));
```

```javascript
Math.sqrt(4);
Math.max(1, 2, 3);
Math.min(1, 2, 3);

Math.trunc(23.3);
Math.floor(23.3);
Math.ceil(23.3);
Math.round(23.3);
```

```javascript
const randIntGenerator = (min, max) =>
  Math.floor(Math.random() * (max - min) + 1) + min;
```

### If, else statements

```javascript
const value = 4;

if (value % 2 == 0) console.log("It is divisible by 2.");
else if (value % 3 == 0) console.log("It is divisible by 3.");
else console.log("It's not divisible by 2 and 3.");
```

`Switch statements`,

```javascript
switch (example) {
  case 1:
    doSomething();
    break;
  default:
    exit();
}
```

`Tertiary operator`,

```javascript
2 == 2 ? console.log("It is 2.") : console.log("It is not 2.");
```

### Nullish coalescing operator and Optional chaining

It is used with `??`, it works on nullish values rather than on falsy values, that is `null` and `undefined`.

`Optional chaining`,

Here it works like this, `if b exists in a then continue`, if it fails `undefined` is returned.

```javascript
if (a?.b) {
  consol.log(b);
} else if (a.c?.(1)) {
  console.log(`c() is executed!`);
}
```

### Loops

`for loop`,

```javascript
for (i = 0; i < 10; i++) {
  console.log(i);
}
```

`while loop`

```javascript
while (true) {
  console.log("This loop will run infinitely,");
}
```

`for of loop`

```javascript
for (const i of numbers) {
  console.log(i);
}

const exampleArray = [1, 2, 3];

for (const [i, el] of exampleArray.entries()) {
  console.log(`${i} = ${el}`);
}
```

`for each loop`

```javascript
const loopExample = [1, 2, 3];

loopExample.forEach((items, index, array) => {
  console.log(`${index} : ${items}, ${array}`);
});

const mapExample = new Map([
  ["a", 1],
  ["b", 2],
]);

mapExample.forEach((value, key, map) => {
  console.log(`${key} : ${value}, ${map}`);
});

const setExample = new Set([1, 1, 2, 3]);

setExample.forEach((value, _, set) => {
  console.log(`${value}`);
});
```

`Looping with object`,

```javascript
const days = {
  monday: 2,
  tuesday: 3,
};

for (const day of Object.keys(days)) {
  console.log(days);
}

for (const date of Object.values(days)) {
  console.log(date);
}

for (const [key, value] of Object.entries(days)) {
  console.log(key, value);
}
```

## Data Structures in JavaScript

### Array

```javascript
const fruits = ["apple", "peach"];

// Or
const otherSetOfFruits = new Array("banana", "pineapple");
```

To access from an array indexing can be used, it's `0` based indexing,

```javascript
const evenNumbers = [2, 4, 6];

console.log(evenNumbers[0]);
```

`Destructuring Array`,

```javascript
const exampleArray = [1, 2, 3, 4];

const [a, b, c, d] = exampleArray;
```

`Methods on Array`,

- `push()`, adds an element at the end of the array,
- `pop()`, removes the last element,
- `unshift()`, adds an element at the beginning of array,
- `shift()`, removes the first element,
- `indexOf()`, return the index of an element,
- `includes()`, returns `true` if element is present, or else `false`,
- `length`, return the length of the array,
- `splice()`, removes the elements from the array from start point to stop,
- `reverse()`, reverses the array,
- `concat()`, joins two array,
- `at()`, alternate to brackets notation,

### Sets

`Set` is collection of unique items,

```javascript
const setExample = new Set([1, 2, 1, 2]);
```

`Methods on Sets`,

- `size`, returns the size,
- `has()`, returns boolean value,
- `add()`, add an item,
- `delete()`, delete an item,
- `clear()`, clear the set,

### Maps

`Map` stores key, value pairs,

```javascript
const mapExample = new Map([
  ["a", 1],
  ["b", 2],
]);
```

For looping through a map, it doesn't require `Object.entries()`, it can be directly destructured.

`Methods on Maps`,

- `size`, returns the size,
- `set()`, add an item,
- `get()`, get an item,
- `delete()`, remove single item,

### Spread and Rest operator

`spread` operator,

```javascript
const exampleArrayOne = [1, 2, 3];
const exampleArrayTwo = [...exampleArrayOne, 4, 5, 6];
```

`rest` operator,

```javascript
const [x, ...other] = exampleArrayOne;
// x = 1, other = [2, 3]
```

### Map, Filter and Reduce methods

Using `map()`,

```javascript
const mapExample = [1, 2, 3];

const mapResult = mapExample.map((item) => item ** 2);
```

Using `filter()`,

```javascript
const filterExample = [1, 2, 3];

const filterResult = filterExample.filter((item) => item > 2);
```

Using `reduce()`,

```javascript
const reduceExample = [1, 2, 3];

const reduceResult = reduceExample.reduce(
  (accumulator, item, index, array) => accumulator + item,
  0
);
```

### find and findIndex methods

Using `find()`, it returns the first element that satisfies the condition, in this case 2.

```javascript
const findExample = [1, 2, 3];

const findResult = findExample.find((item) => item > 1);
```

Using `findIndex()`, it is same as `find()` but returns the index,

### Some and Every method

Both these methods return a `boolean value`,

Using `some()`,

```javascript
const someExample = [1, 2, 3];

const someResult = someExample.some((item, index, array) => item > 0);
```

Using `every()`,

```javascript
const everyExample = [1, 2, 3];

const everyResult = everyExample.every((item, index, array) => item > 0);
```

### Flat and FlatMap methods

```javascript
const flatExample = [1, 2, 3, [4, 5, [6, 7]]];

const flatResult = flatExample.flat(2);
```

Here `flatMap()`, first works as `map()` method and then works as `flat()` method,

### Sorting array

`sort()` function could be used but it doesn't work as intended on numbers, so instead a callback function needs to be given to sort,

```javascript
const sortExample = [1, 3, 2];

sortExample.sort(() => {
  if (a > b) return 1;
  if (b > a) return -1;
});
```

### Creating and Filling arrays

`fill()` method accepts arguments in this form, `value`, `start`, `stop`,

```javascript
const arrExample = new Array(7);

arrExample.fill(1, 3, 5);

const arrAnotherExample = Array.from({ length: 7 }, () => 1);
```

### Strings

`String` is a sequence of characters, like an `array`, `string` has same methods on it.

`Other methods on strings`,

- `lastIndexOf()`, returns last index,
- `slice()`, slice the string (start to stop, but stop not included),
- `toLowerCase()`, converts to lower case,
- `toUpperCase()`, converts to upper case,
- `trim()`, removes whitespace,
- `replace()`, replace a value with given value,
- `startWith()`, returns a boolean value,
- `endsWith()`, returns a boolean value,
- `split()`, splits a string with delimiter provided,
- `join()`, joins strings with a value,
- `padStart(), padEnd()`, pad a string with a given value,
- `repeat()`, replicate string,

## Working with Dates

```javascript
console.log(new Date());
```

`Methods on Dates`,

- `getFullYear()`, returns the year,
- `getMonth()`, returns the month, it is `0` based,
- `getDay()`, returns the date, day of the week,
- `getDate()`, returns date,
- `getHours()`, returns hours,
- `getMinutes()`, returns minutes,
- `getSeconds()`, returns seconds,
- `toISOString()`, Converts the date string to ISO string,
- `getTime()`, returns time stamp, also `Date.now()`

### Internalization API

```javascript
const options = {
  hours: "numeric",
  minutes: "numeric",
};

const locale = navigator.language;

const dateInCountry = new Intl.DateTimeFormat(locale, options).format(
  new Date()
);
```

```javascript
const options = {
  style: "unit",
};

const locale = navigator.language;

const numberInCountry = new Intl.NumberFormat(locale).format(2093839.938);
```

### Timers

`setTimeOut()`,

```javascript
setTimeOut(() => {
  console.log("Executes after 3 seconds,");
}, 3000);
```

`setTimeInterval()`,

```javascript
setTimeInterval(() => {
  console.log("Executes after every 3 seconds,");
}, 3000);
```

`clearTimeOut()` and `clearTimeInterval()` are used to remove the timers,

## Functions

`JS` has `first class functions`, this means that functions are simply values, and `higher order function` is the one which accepts a function as argument and then returns a function,

```javascript
function square(n) {
  let value = square ** 2;
  return square;
}
```

The functions can also be assigned to variables as,

```javascript
const greet = function (user) {
  return `Hello ${user}!!`;
};

greet("root"); // Calling the function
```

`Arrow functions`,

```javascript
const isEven = (n) => n % 2 === 0;
```

In `Arrow functions` a single line doesn't need a return statement, but if there are multiple lines then it should be enclosed within `{}` with `return` keyword.

`Functions returning functions`,

```javascript
const greet = function (greeting) {
  return function (user) {
    console.log(`${greeting} ${user}!!!`);
  };
};

const returningFunction = greet("Hi");
returningFunction("root");

greet("Hi")("root");
```

### `call`, `apply` and `bind` methods

Here when the `a.returnValue` is assigned, the `getValue` is just a function and it doesn't know about `this` keyword, to solve this we use `call`, `apply` and `bind` method, Here the first parameter is for the `this` keyword,

```javascript
const a = {
  value: 23,
  returnValue(user) {
    console.log(`${this.value} returned to ${user}. `);
  },
};

const b = {
  value: 24,
};

const getValue = a.returnValue;
```

Using `call()`, after passing the values, now the `this` keyword points to the first argument,

```javascript
getValue.call(b, "root");
```

Using `apply()`, it is similar to `call()` but accepts arguments as array,

```javascript
getValue.apply(b, ["root"]);
```

Using `bind()`, it binds the `this` keyword and returns a new function, the `call()` and `apply()` methods calls the function, but since `bind()` returns a new function it is used to pass arguments in callback functions.

```javascript
const returnFunction = getValue(b);

header.addEventListener("click", returnFunction.bind("root"));
```

### Immediately Invoked Function Expressions

The `Immediately Invoked Function Expressions` are used to create a scope,

```javascript
(function runOnce() {
  console.log("It will run only once.");
})();

(() => console.log("It will run only once."))();
```

### Closure

A function has access to variable environment of the execution context in which it was created, and it is called as `closure`.

Here even though the `closureExample` is already returned, the returned function `closureFunction` still has access to the `counter` variable.

```javascript
const closureExample = function () {
  let counter = 0;

  return function () {
    counter++;
    console.log(`${counter}`);
  };
};

const closureFunction = closureExample();

closureFunction();
```

## DOM

`DOM` is structured representation of `HTML` documents, it allows the `JS` to access `HTML` elements and styles to manipulate them.

```javascript
const header = document.querySelector("header");

const headerValue = header.value;

header.textContent = "It is a header element.";

header.innerHTML = "<h1>inner HTML</h1>";
```

`Event Listeners` can be added with `addEventListener()` function,

```javascript
button.addEventListener("click", function () {
  console.log("It's a callback function.");
});
```

`Node` is represented by a javascript object, then it has `elements`, `text`, `comment`, `document`.

### Selecting, Creating and Deleting elements

```javascript
const html = document.documentElement;
const head = document.head;
const body = document.body;
```

`Selecting`, The `querySelectorAll` returns a `Node List`, but `getElementsByTagName` returns a `HTML Collection` it is a live collections (dynamic),

```javascript
document.querySelector(".header");
document.querySelectorAll(".header");

document.getElementById("#header");
document.getElementsByTagName("button");

document.getElementsByClassName("header");
```

### Creating and Inserting

```javascript
const buttonBox = document.createElement("div");

header.prepend(buttonBox);
header.append(buttonBox.cloneNode(true));
header.before(buttonBox);
header.after(buttonBox);

buttonBox.remove();

insertAdjacentHTML("beforebegin", html);
```

### Styling in DOM

Manipulating `CSS Styles`,

```javascript
header.style.backgroundColor = "red";
```

Working with `classes`,

```javascript
header.classList.add("hidden");
header.classList.remove("hidden");
header.classList.toggle("hidden");

header.classList.contains("hidden");

getComputedValue(header).color;

document.documentElement.style.setProperty("--color-primary", "#fff");

headerImg.alt;
headerImg.className;
headerImg.getAttribute("custom");
headerImg.setAttribute("custom", "value");
```

Special data values can be added as attribute, `data-value-is = 3`,

```javascript
headerImg.dataset.valueIs;
```

### Smooth Scrolling

Current scroll (x / y), `window.pageXOffset`, `window.pageYOffset`,
Current viewport width/height, `document.documentElement.clientWidth`, `document.documentElement.clientHeight`,

```javascript
const coordinates = header.getBoundingClientRect();

window.scrollTo({
  left: coordinates.left + window.pageXOffset,
  top: coordinates.top + window.pageYOffset,
  behavior: "smooth",
});
```

`modern way`,

```javascript
header.scrollIntoView({ behavior: "smooth" });
```

### Event Propagation

It has `capturing phase`, `target phase`, and `bubbling phase`, the `event listeners` in javascript only listen to event in `bubbling phase`.

### DOM Traversing

```javascript
const h1 = document.querySelector("h1");
```

Selecting children,

```javascript
h1.querySelector("span");

h1.childNodes;
h1.children;
h1.firstElementChild;
h1.lastElementChild;
```

Selecting Parent,

```javascript
h1.parentNode;
h1.parentElement;

h1.closest("header");
```

Selecting Siblings,

```javascript
h1.previousElementSibling;
h1.nextElementSibling;

h1.previousSibling;
h1.nextSibling;
```

### Passing arguments to event handler functions

use `bind()` method to pass arguments to event handler functions.

### Intersection Observer API

Here it check if `header` is intersecting the viewport at threshold of `0.1`.

```javascript
const obsCallBack = function (entries, observer) {
  entries.forEach((item) => console.log(item));
};

const obsOptions = {
  root: null,
  threshold: 0.1,
};

const observer = new intersectionObserver(obsCallBack, obsOptions);
observer.observe(header);
```

### LifeCycle of DOM events

```javascript
document.addEventListener("DOMContentLoaded", function () {
  console.log("Loaded.");
});

window.addEventListener("load", function () {
  console.log("Page loaded.");
});

window.addEventListener("beforeunload", function (e) {
  e.preventDefault();
  e.returnValue = "";
});
```

## Object Oriented Programming

It's a paradigm based on the concept of objects. It has `classes` and `instances`. An `instance` is created from a class.

Four fundamental concepts,

- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

### Creating Objects

```javascript
const student = {
  fullName: "user",
  age: 21,

  getAge: function () {
    return age;
  },
};

console.log(student.fullName);
console.log(student["age"]);
```

The values can be accessed through `dot` or `bracket` notation,

`Destructuring Objects`,

```javascript
const { fullName: studentName, age: studentAge } = student;
```

### Constructor Functions

In javascript all objects are linked to `prototypes`. The methods the `prototypes` contain can be inherited by all the `objects` linked to it. It's called as `Prototypal inheritance`.

```javascript
const greet = function (user) {
  this.user = user;

  console.log(`hello ${user}`);
};

const user = new greet("Alex");

console.log(user instanceof greet);
```

### Prototypes

```javascript
greet.prototype.ask = function () {
  console.log("What is your nick name?");
};

user.ask();
```

```javascript
console.log(user.__proto__);
console.dir(user.prototype.constructor);
```

### ES6 Classes

```javascript
class greet() {
  constructor() {
    console.log("Runs first");
  }

  sayHello() {
    console.log("Hello!!");
  }
}

```

### Setters and Getters

```javascript
const numbers = {
  const arr = [1, 2, 3];

  get last(){
    return arr.at(-1);
  }

  set last(value){
    arr.push(value)
  }
};

console.log(numbers.last);
numbers.last = 4;
```

### Static Methods

The `methods` are created directly for constructor, and not for object / prototype.

```javascript
Array.from(document.querySelectorAll("h1"));

[1, 2, 3].from(); // Doesn't work
```

`this` keyword points to the constructor.

```javascript
greet.age = function (age) {
  console.log("Your age is " + age + ".");
};
```

### Object.create()

```javascript
const greet = {
  sayHello() {
    console.log("hello !");
  },
};

const user = Object.create(greet);
```

## Asynchronous JavaScript

In JavaScript most code is `synchronous`, it is executed line by line, waiting for the previous code to finish executing.

`setTimeOut()` works in `asynchronous` way, it do not block the other code,so `asynchronous` is `non-blocking`.

### AJAX

`Asynchronous JavaScript And XML`, it allows to communicate with remote web servers in `asynchronous` way.

```javascript
const request = new XMLHttpRequest();
request.open("GET", "https://api.com");
request.send();

request.addEventListener("load", function () {
  console.log(this.responseText);

  const data = JSON.parse(this.responseText);
});
```

### Promises and `fetch` API

`Promise` is an object that is used as a placeholder for future result of an asynchronous operation.

```javascript
const request = fetch("https://api.com");
```

### Consuming a Promises

```javascript
const request = fetch("https://api.com")
  .then(function (response) {
    return response.json();
  })
  .then(function (data) {
    console.log(data);
  });
```

### Handling Rejected Promises

`then()` can accept two callback functions, one for accepted promises, and another one for rejected promises,

If the promises are chained then one single `catch()` method can be used at last promise.

```javascript
const request = fetch("https://api.com")
  .then(
    (response) => response.json(),
    (err) => console.log(`Error : ${err}`)
  )
  .then((data) => console.log(data));
```

```javascript
const request = fetch("https://api.com")
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
    return fetch("https://api.in");
  })
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((err) => console.log(err));
```

`Throwing Errors Manually`,

```javascript
const request = fetch("https://api.com")
  .then((response) => {
    if (response.ok == false) throw new Error("Error");
    return response.json();
  })
  .then((data) => {
    console.log(data);
  });
```

### Building Promises

```javascript
const promiseExample = new Promise(function (resolve, reject) {
  let a = 2;
  if (a === 2) {
    resolve("This promise is resolved.");
  } else {
    reject(new Error("This promise is rejected."));
  }
});

promiseExample.then((res) => console.log(res)).catch((err) => console.log(err));
```

### Async and Await

```javascript
const request = async function () {
  const res = await fetch("https://api.com");
  const data = await res.json();
};
```

`Error Handling`,

```javascript
const request = async function () {
  try {
    const res = await fetch("https://api.com");
    const data = await res.json();
  } catch (err) {
    console.log(err);
  }
};
```

### Returning from Async

```javascript
const request = async function () {
  const res = await fetch("https://api.com");
  const data = await res.json();
  return "Fetch completed.";
};

request.then((data) => console.log(data));
```

### Running promises in parallele

```javascript
async function(){
  const data = await Promise.all([fetchSomething(), fetchSomething()])
  console.log(data)
}
```

## Modern JavaScript Development

A `module` is a reusable piece of code, that encapsulates the implementation details, these are imported synchronously. To use it we need to link it to the `html` file using,

```html
<script type="module" defer src="index.js"></script>
```

`module_example.js`

```javascript
console.log("From module_example.js");

export const greet = function () {
  console.log("Hello From Module !");
};
```

```javascript
import { greet } from "module_example.js";

greet();
```

`export const ...` is called as `named export`, `export default function () ...` is called as `default export`.

### Using `await` in outside of `async` functions

```javascript
const res = await fetch("http://api/v1/data");
const data = await res.json();
```

Although it blocks the entire execution.

### Common JS Module

```javascript
export.greet = function(){
  console.log("Hello World !")
}
```

```javascript
const file_example = require("file_example");
```

### Using parcel and babel

Use parcel for development,`parcel index.html`, to build use `parcel build index.html`.

For poly filling use `core-js/stable` and `regenerator-runtime/runtime` modules.

```javascript

```
