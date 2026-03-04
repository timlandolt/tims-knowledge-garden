---
{"dg-publish":true,"permalink":"/knowledge/named-java-script-arguments/"}
---

## Object deconstruction
To understand how named (and unordered) arguments in JavaScript work, we have to understand the principles behind object deconstruction in JavaScript.

Basically you can split up an object into multiple single variables using object deconstruction. The syntax is as followed:

```javascript
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50
};

let {firstName, lastName} = person; // Object deconstruction

console.log( firstName ); //=> John
console.log( lastName ); //=> Doe
```

## Object deconstruction with function arguments

The idea behind named arguments is that instead of multiple arguments you pass in one object. The properties can easily be accessed, because they get interpreted as arguments.

```javascript
function example({ x, y, z }) {
  console.log(x);
  //...
}

example({
  z: 1,
  x: 2,
  y: 3,
})
```

>[!important] Advantages
>- You get a better overview of the values you pass in
>- You can enter the values in any order
>- Values with default values can be in any position

## Passing the arguments into super constructor using Property shorthand

Another concept that gets handy in this context is the property shorthand. That means that you can pass variables into an object without having to explicitly use properties if the name of said variables are the same as the property name:

```js
const firstName = "John";
const lastName = "Doe";

const person = {
  firstName,
  lastName,
};


console.log( person.firstName ); //=> John
console.log( person.lastName ); //=> Doe
```

You can use this feature to easily pass values into a super constructor:

```js
class Person {
  constructor({ firstName, lastName }) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}

class Student extends Person {
  constructor({ firstName, lastName, teacher }) {
    super({ firstName, lastName });
    this.teacher = teacher;
  }
}
```
