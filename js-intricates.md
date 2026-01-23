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
