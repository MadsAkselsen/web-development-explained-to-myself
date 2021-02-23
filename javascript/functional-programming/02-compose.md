# Compose

Functional composition is when you take two or more functions, and make one a single function out of them.

When you compose functions into a single function call, you can start using them as pipelines of specific behavior. These pipelines can then take the result of each function that comprises it, and use it as the argument to the next function in the pipeline.

## Example with reduce()

The following factoryFunc() function takes in n amount of functions and runs `val` through each of them - just like factory

```js
const factoryFunc = (...args) => {
  return args.reduce((f, g) => (val) => {
    return f(g(val));
  });
};
```

```js
const func1 = (val) => {
  return val + 4;
};

const func2 = (val) => {
  return val + 4;
};

const func3 = (val) => {
  return val + 5;
};

const composed = factoryFunc(func1, func2, func3);

console.log('without val:', composed);
console.log('with val:', composed(2));
```

**First iteration:**

  1. Values are inserted into the parameter of the reducer:
  
     ```js
     (nothing, func1)
     ```
  
     This means
     - `f = nothing`
     - `g = func1(val)`

  2. The return of this iteration becomes:
  
     ```js
     (val) => return {func1(val)}
     ```

     This return value is f (the accomulator) in the next iteration

**Second iteration:**

1. Values are inserted into the parameter of the reducer:

     ```js
     ((val) => return {func1(val)}, func2)
     ```

     This means
     - `f = (val) => return {func1(val)}`
     - `g = func2(val)`

     Remember g goes into f(val): `f = (func2) => return {func1(func2)}`

2. The return of this iteration becomes:

      ```js
     (val) => return {func1(func2(val))}
     ```

     This return value is f (the accomulator) in the next iteration

**Third iteration:**

1. Values are inserted into the parameter of the reducer:

     ```js
     ((val) => return {func1(func2(val))}, func3)
     ```

     This means
     - `f = (val) => return {func1(func2(val))}`
     - `g = func3(val)`

     Remember g goes into f(val): `f = (func3) => return {func1(func2(func3(val)))}`

2. The return of this iteration becomes:

      ```js
     (val) => return {func1(func2(func3(val)))}
     ```

The return value of `const composed = factoryFunc(func1, func2, func3)` is therefore `(val) => return {func1(func2(func3(val)))}`.

`composed(2)` is therefore `(2) => return {func1(func2(func3(2)))}`

## pipe
