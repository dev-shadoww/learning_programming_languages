# Learning TypeScript

## Introduction

`TypeScript` is just `javascript` + `type system`, install `ts-node` and `typescript` packages,

```bash
npm -g typescript ts-node
```

to execute `TypeScript`,

```bash
tsc index.ts && node index.js
```

or,

```bash
ts-node index.ts
```

## Type System

`Type` is a easy way to refer to the different properties + functions that has a value,

## Type annotations

`Type Annotations`, code which tell the typescript what type of value a variable will refer to, `Type Interface`, typescript tries to figure out what type of value a variable refers to.

### Type Annotations with Variables

```typescript
const vehicles: number = 6;
const speed: string = "fast";
const isFast: boolean = true;
const canFly: null = null;
const nothing: undefined = undefined;
const now: Date = new Date();
```

```typescript
const colors: string[] = ["red", "yellow"];

class Car {}

const suzuki: Car = new car();

const point: { x: number; y: number } = {
  x: 10,
  y: 20,
};
```

```typescript
const printNumber: (i: number) => void = (i: number) => {
  console.log(i);
};
```

If declaration and initialization of a variable are on the same line then the typescript will figure out the type, this is known as `type inference`.

### Type Annotations with Functions and Objects

```typescript
const add = (a: number, b: number): number => {
  return a + b;
};

function subtract(a: number, b: number): number {
  return a - b;
}
```

```typescript
const greet = (s: string): void => {
  console.log(`Hello ${s}!`);
};

const throwError = (m: string): never => {
  throw new Error(m);
};
```

```typescript
const days = {
  today: "monday",
  tomorrow: "tuesday",
};

const theDays = (daysAre: {today: string, tomorrow: string}) => {
  console.log(daysAre:today, daysAre:tomorrow);
}

const theDaysWithDestructuring = ({today, tomorrow}: {today: string, tomorrow: string}) => {
  console.log(daysAre:today, daysAre:tomorrow);
}
```

```typescript
const person = {
  age: 20,
};

const { age }: { age: number } = person;
```

### Arrays, Tuples in typescript

`Arrays`,

```typescript
const fruits: string[] = ["apples", "pineapples"];

const calender: (string | Date)[] = ["today", new Date()];
```

`Tuples`,

```typescript
type Drink = [string, number];

const soda: Drink = ["white", 40];
```

### Interfaces

`Interfaces` are creating a new type, describing the property names and value types of an object.

```typescript
interface Student {
  name: string;
  age: number;
  summary(): string;
}

const newStudent = {
  name: "user",
  age: 20,
  summery(): string {
    return this.name;
  },
};

const printStudentData = (student: Student): void => {
  console.log(`Name is ${student.name} and age is ${student.age}.`);
};
```

### Working with classes

Method `modifiers`,

- `Public`, The methods can be called from anywhere
- `Private`, The methods can be called only from the other methods of that class
- `Protected`, The methods can be called by other methods of the same class or child class

```typescript
class Vehicle {
  genericWeight = 1000;

  constructor(public color: string) {}

  protected drive(): void {
    console.log("Driving");
  }

  public getWeight(): number {
    return genericWeight;
  }
}

const car = new Vehicle("red");
car.drive();
console.log(car.color);
```
