# Spread Operator (...)
**Ex1: Dùng với list**
```js
const a = [1, 2, 3];
const b = [...a, 4]; // b = [1, 2, 3, 4];
```
**Ex2: Dùng với Object**
```js
const user = { name: "An", age: 20 };
const newUser = { ...user, age: 21 }; // { name: "An", age: 21 }
```