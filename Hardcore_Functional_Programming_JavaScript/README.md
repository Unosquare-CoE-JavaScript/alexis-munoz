# Hardcore Functional Programming in Javascript

## Pure Functions

The pure functions are functions that have no side effects and no external dependencies.

Advantages:

- Reliable
- Portable
- Reusable
- Testable
- Composable
- Properties / Contract

```js
const add = (a, b) => {
  return a + b;
};
```

## Not Pure Functions

The not pure functions are functions that have side effects or ahve external dependencies.

```js
const add = (a, b) => {
  return a + b + localStorage.getItem('c');
};
```

### Currying functions

Currying is a technique of transforming a function with multiple arguments into a sequence of functions, each with a single argument.

```js
const m = z => (y, x) => z + x + y;
const curryedAdd = m(1);
console.log(curryedAdd(2, 3)); // 6
```

### Composition functions

Compose is a function that takes two functions or moew as arguments and returns a function that is their composition.

```js
compose = (f, g) => x => f(g(x));
```

So we can put it in the following way:

```js
const compose = (...fns) => x => fns.reduceRight((v, f) => f(v), x);
const addTen = x => x + 10;
const multiplyByTwo = x => x * 2;
const addTenAndMultiplyByTwo = compose(
    multiplyByTwo
    addTen, 
);
console.log(addTenAndMultiplyByTwo(5)); // 20
```

### Composition is Dot Chaining

Composition is also known as dot chaining.

```js
const cleanup => str => 
str.split(' ')
    .map(word => word.toUpperCase())
    .reverse()
    .join(' ');
```

### Pipe function

The pipe function is a composition function that takes a list of functions and returns a function that is the composition of those functions. The first difference between pipe and compose is that pipe is right-associative, while compose is left-associative.

```js
const pipe = (...fns) => x => fns.reduce((v, f) => f(v), x);
const addTen = x => x + 10;
const multiplyByTwo = x => x * 2;
const addTenAndMultiplyByTwo = compose(
    addTen, 
    multiplyByTwo
);
console.log(addTenAndMultiplyByTwo(5)); // 20
```

## Identity Functor

The indentity functor is a functor that wraps a value.

```js
const Box = x => ({
   map: f => Box(f(x)), 
})
```

You can do nested functors with the identity functor.

```js
const applyDiscount = (price, discount) =>
  Box(moneyToFloat(price))
     .fold(cents => Box(percentToFloat(discount))
      .fold(savings => cents - (cents * savings)))
```

### The Either Monad

The type Either is a functor and a monad, it has both a map, a chain method, and a fold method. The Either type respects function purity and is effectively an if else statement, but inverted.

  ```js
  const Right = x =>
  ({
    chain: f => f(x),
    map: f => Right(f(x)),
    fold: (f, g) => g(x),
    toString: () => `Right(${x})`
  });

const Left = x =>
  ({
    chain: f => Left(x),
    map: f => Left(x),
    fold: (f, g) => f(x),
    toString: () => `Left(${x})`
  });

const fromNullable = x =>
    x != null ? Right(x) : Left(null);

 fromNullable(2).map(x => x * x).fold(x => x, x => x); // 4
```

### Task monad

Task monad is the functional equivalent of promise. Similarly to promise, Task takes resolve and reject functions, but in reversed order. A Task monad only starts running once it reaches the fork method, and this way avoids race conditions.

```js
// Create new task that will resolve with 'hello world' after 1000 ms
const t = new Task((reject, resolve) => {
  setTimeout(() => resolve('hello world'), 1000)
});

// The effect only happens when `fork` is called.
t.fork(
  // Rejected handler
  (x) => console.error(x),
  // Resolved handler
  (s) => console.log(s)
);
```
