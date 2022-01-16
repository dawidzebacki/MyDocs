# JS

* Unique values

```js
const myArray = ['a', 1, 'a', 2, '1'];
const unique = [...new Set(myArray)];
console.log(unique); // unique is ['a', 1, 2, '1']
```