---
title: How To Use Async/Await (JavaScript)
published: true
---

# Introduction

Often in web development, we need to handle asynchronous actions— actions we can wait on while moving on to other tasks. We make requests to networks, databases, or any number of similar operations. JavaScript is non-blocking: instead of stopping the execution of code while it waits, JavaScript uses an event-loop which allows it to efficiently execute other tasks while it awaits the completion of these `async`hronous actions.

Originally, JavaScript used callback functions to handle `async`hronous actions. The problem with callbacks is that they encourage complexly nested code which quickly becomes difficult to read, debug, and scale. With ES6, JavaScript integrated native promises which allow us to write significantly more readable code. JavaScript is continually improving, and ES8 provides a new syntax for handling our `async`hronous action, `async`...await. The `async`...await syntax allows us to write `async`hronous code that reads similarly to traditional synchronous, imperative programs.

The `async`...await syntax is syntactic sugar— it doesn’t introduce new functionality into the language, but rather introduces a new syntax for using promises and generators. Both of these were already built in to the language. Despite this, `async`...await powerfully improves the readability and scalability of our code.

# The `async` Keyword
The `async` keyword is used to write functions that handle `async`hronous actions. We wrap our `async`hronous logic inside a function prepended with the `async` keyword. Then, we invoke that function.

```javascript
`async` function myFunc() {
  // Function body here
};

myFunc();
```

We’ll be using `async` function declarations throughout this lesson, but we can also create `async` function expressions:

```javascript
const myFunc = `async` () => {
  // Function body here
};

myFunc();
```

``async`` functions always return a promise. This means we can use traditional promise syntax, like `.then()` and `.catch` with our `asyn`c functions. An ``async`` function will return in one of three ways:

* If there’s nothing returned from the function, it will return a promise with a resolved * value of `undefined`.
* If there’s a non-promise value returned from the function, it will return a promise resolved to that value.
* If a promise is returned from the function, it will simply return that promise

```javascript
`async` function fivePromise() { 
  return 5;
}

fivePromise()
.then(resolvedValue => {
    console.log(resolvedValue);
  })  // Prin
  ```

In the example above, even though we return `5` inside the function body, what’s actually returned when we invoke `fivePromise()` is a promise with a resolved value of `5`.



# The await Operator
In the last exercise, we covered the `async` keyword. By itself, it doesn’t do much; `async` functions are almost always used with the additional keyword `await` inside the function body.

The `await` keyword can only be used inside an `async` function. `await` is an operator: it returns the resolved value of a promise. Since promises resolve in an indeterminate amount of time, `await` halts, or pauses, the execution of our `async` function until a given promise is resolved.

In most situations, we’re dealing with promises that were returned from functions. Generally, these functions are through a library, and, in this lesson, we’ll be providing them. We can `await` the resolution of the promise it returns inside an `async` function. In the example below, `myPromise()` is a function that returns a promise which will resolve to the string `"I am resolved now!"`.

```javascript
`async` function `async`FuncExample(){
  let resolvedValue = await myPromise();
  console.log(resolvedValue);
}

`async`FuncExample(); // Prints: I am resolved now!
```

Within our `async` function, `asyncFuncExample()`, we use await to halt our execution until `myPromise()` is resolved and assign its resolved value to the variable `resolvedValue`. Then we log `resolvedValue` to the console. We’re able to handle the logic for a promise in a way that reads like synchronous code.





# Writing async Functions

We’ve seen that the `await` keyword halts the execution of an async function until a promise is no longer pending. Don’t forget the `await` keyword! It may seem obvious, but this can be a tricky mistake to catch because our function will still run— it just won’t have the desired results.

We’re going to explore this using the following function, which returns a promise that resolves to `'Yay, I resolved!'` after a 1 second delay:

```javascript
let myPromise = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve('Yay, I resolved!')
    }, 1000);
  });
}
```

Now we’ll write two `async` functions which invoke `myPromise()`:

```javascript
async function noAwait() {
 let value = myPromise();
 console.log(value);
}

async function yesAwait() {
 let value = await myPromise();
 console.log(value);
}

noAwait(); // Prints: Promise { <pending> }
yesAwait(); // Prints: Yay, I resolved!
```

In the first `async` function, `noAwait()`, we left off the await keyword before `myPromise()`. In the second, `yesAwait()`, we included it. The `noAwait()` function logs Promise { <pending> } to the console. Without the await keyword, the function execution wasn’t paused. The `console.log()` on the following line was executed before the promise had resolved.

Remember that the await operator returns the resolved value of a promise. When used properly in `yesAwait()`, the variable value was assigned the resolved `value` of the `myPromise()` promise, whereas in `noAwait()`, `value` was assigned the promise object itself.