# Learning JavaScript

## Object Oriented Programming

It's a paradigm based on the concept of objects. It has `classes` and `instances`. An `instance` is created from a class.

Four fundamental concepts,

- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

In javascript all objects are linked to `prototypes`. The methods the `prototypes` contain can be inherited by all the `objects` linked to it. It's called as `Prototypal inheritance`.

### Constructor Functions

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
