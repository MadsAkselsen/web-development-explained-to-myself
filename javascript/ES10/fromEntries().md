# Object.fromEntries()

Converts key-value pairs into an object

key-value pairs can be a map() or an array of key-value pairs

```js
const entries = new Map([
  ['foo', 'bar'],
  ['baz', 42]
]);

const obj = Object.fromEntries(entries);

console.log(obj);
// expected output: Object { foo: "bar", baz: 42 }
```

Object.entries() is the opposite - it converts an object into an array of key-value pairs