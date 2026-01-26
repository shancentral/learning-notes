# JS Intricates

```js
// var leaks outside of block scope
// Hence use let/const

for (var a = 0; a < 10; a++) {}
console.log(a); // 10
```
---
```js
const arr = [1];
arr[0] = 2;

console.log(arr); // [2]
```
---
```js
// syntax to return an object

const func = () => ({ test: "test" })
```
---
```js
// syntax to return an object

const func = () => ({ test: "test" })
```
---
```js
// dynamic object name binding
const testN = "test1";

const state = {
  test1: 1,
  test2: 2
}

console.log({...state, [testN]: state[testN] + 1})
// { test1: 2, test2: 2 }
```
