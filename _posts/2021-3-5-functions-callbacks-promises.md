---
layout: post
title: Functions, Callbacks & Promises
---

## Functions

Functions are reusable blocks of code designed to perform a particular task. 

#### Function Declarations:

Function declarations make it so that the function can be called and used. They are defined with special parameters. The first way to declare a function is the more traditional and classic way of doing it. You declare it by using the `function` keyword:

```javascript
function myFunction() {}
```

A second way of declaring functions is by assigning the function to a value. This is called a function expression:

```javascript
const myFunction = function() {}
```

And lastly, a more modern way to declare a function is by using the arrow function and dropping the `function` keyword:

```javascript
const myFunction = (parameter) => {}
```

#### How to return a value from a function

The `return` statement ends function execution and specifies a value to be returned to the function caller:

```javascript
function myFunction(a) {
    let b = a + 1

    return b
}
```

#### How to accept a value into a function

Functions accept values through parameters:

```javascript
function myFunction(param1, param2) {
    return param1 + param2
}
myFunction(1, 2);
// returns 3
```

## Callbacks

Accoriding to MDN, a callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action. They can be synchronous (executed immediately) or asynchronous (executed after some other action). You'll find the asynchronous way used more often, especially when fetching data from APIs. A good example is a callback executed inside a `.then()` block chain at the end of a promise which leads us to the next section. 

## Promises

Again, according to MDN, a promise represents the eventual completion (or failure) of an asynchronous operation. A `Promise` can have one of three states:

- pending: initial state, neither fulfilled nor rejected
- fulfilled: meaning that the operation was completed successfully
- rejected: meaning that the operation failed

```javascript
const delayedMessage = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve('This message has been delayed');
    }, 3000);
});
```

In the example above, if the promise is fulfilled and resolved, the delayed message will appear after 3 seconds.

#### Async and Await Syntax

Async and await act as syntactic sugar and make promises easier to read and write. It also lets you avoid `.then()` chaining which can get pretty complicated. This can be super helpful when fetcing data from an API.

```javascript
async function fetchApiData() {
    let response = await fetch('some url') 
    let data = await response.json();
    return data
}
```