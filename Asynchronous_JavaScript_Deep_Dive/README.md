# Asynchronous JavaScript Deep Dive


## Synchronous code

Synchronous code is code that runs in the same thread as the main thread. JavaScript is a synchronous language, which means that all code is executed in the same thread.

#### Pros:   
- Easy to understand
- Easy to write
- Easy to debug
- Easy to reuse
- Easy to test

#### Cons:
- Less performant
- May create blocking code


## Asynchronous code

Asynchronous code is code that runs in a separate thread from the main thread.

### Pros:
- Very performant
- Eliminates code blocking

### Cons:
- Harder to write
- Difficult to reason about

## Event Loop
The event loop is an algorithm that constantly checks the call stack to see if there are any function calls that need to be run. When the call stack is empty, the first entry in the callback queue is pushed onto the call stack to complete execution. This happens until the queue is empty.

## Callbacks
The callback is a function that will be called or invoked when a certain event occurs. For example, when a user clicks a button, the callback function is called.

```js
document.addEventListener('click', function() {
  console.log('clicked');
});
```
## Problems with callbacks
 
- Callback hell
- Difficult to reason about
- Inversion of control

## Promises

Promises are javascript objects that represent the eventual result of an asynchronous operation.

They are coded as it follows:

```js
const promise = new Promise(function(resolve, reject) {
  // do something
});
```

The promise can be concluded with a `.then` method. The `.then` method takes a callback function that will be called when the promise is resolved. The `catch` method will be called when the promise is rejected and the `finally` method will be called when the promise is resolved or rejected, useful for cleanup.


```js
promise.then(function(result) {
  // do something
});
```

The promises can have one of the following states:

- **pending**: Initial state, neither fulfilled nor rejected.
- **fulfilled**: meaning that the operation was completed successfully.
- **rejected**: meaning that the operation failed.

## Fetch Web API
The fetch API is a web API that allows you to fetch data from a server. It's part of the window object and not a feature of javascript language.

```js
fetch('https://api.github.com/users/alexeikmun')
  .then(response => response.json())
  .then(data => console.log(data));
```

We can add more options to the fetch method by passing an object as the second parameter.

```js
fetch('https://api.github.com/users/alexeikmun', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'alexeikmun'
  })
})
  .then(response => response.json())
  .then(data => console.log(data));
```

## Promise static methods
### Promise.all
The `Promise.all` method takes an array of promises and returns a new promise that is fulfilled when all the promises in the array are fulfilled.

```js
Promise.all([
  fetch('https://api.github.com/users/alexeikmun'),
  fetch('https://api.github.com/users/user2')
])
  .then(responses => Promise.all(responses.map(response => response.json())))
  .then(data => console.log(data));
```

### Promise.race
The `Promise.race` method takes an array of Promises and returns a new promise that is fulfilled when the first promise in the array is resolved.

```js
Promise.race([
  fetch('https://api.github.com/users/alexeikmun'),
  fetch('https://api.github.com/users/user2')
])
  .then(response => response.json())
  .then(data => console.log(data));
```

### Promise.allSettled
The `Promise.allSettled` returns a promise that resolves after all of the given promises have either fulfilled or rejected, with an array of objects that each describes the outcome of each promise.

```js
Promise.allSettled([
  fetch('https://api.github.com/users/alexeikmun'),
  fetch('https://api.github.com/users/user2')
])
  .then(responses => Promise.allSettled(responses.map(response => response.json())))
  .then(data => console.log(data));
```

### Promise.any
The `Promise.any` method takes an array of promises and returns a new promise that is fulfilled when the first promise in the array is resolved.

```js
Promise.any([
  fetch('https://api.github.com/users/alexeikmun'),
  fetch('https://api.github.com/users/user2')
])
  .then(response => response.json())
  .then(data => console.log(data));
```

## Async Await

The Async Await is a new way to write asynchronous code in javascript. It is a new way to write asynchronous code in javascript. It is a syntactic sugar for the promises.

```js
async function getUser() {
  const response = await fetch('https://api.github.com/users/alexeikmun');
  const data = await response.json();
  console.log(data);
}
```

## Generators

Generators are special functions that can generate multiple values by using the `yield` keyword. The definition of a generator is similar to a function except that it uses the symbol `*` like: `function*()` instead of `function()`.

```js
 function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}
```

### Make generator iterable
Once a generator is created, it can be used in a for..of loop.


```js
  for (let value of generateSequence()) {
    console.log(value);
  }
```

Or we can use the `.next()` method.
  
  ```js
    let generator = generateSequence();
    console.log(generator.next());
    console.log(generator.next());
  ```

### Convert arrays and strings to generators

By using the Symbol.iterator method, we can convert an array or a string into a generator.

```js
  let array = [1, 2, 3];
  let generator = array[Symbol.iterator]();
  console.log(generator.next());
```

*Note: This is only possible with arrays and strings.*