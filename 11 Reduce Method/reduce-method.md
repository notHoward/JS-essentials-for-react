# The Array `reduce()` Method

---

## 1. Overview

The `reduce()` method **reduces an array to a single value** by applying a function to each element in the array.

* Original array **is not modified**
* Can calculate sums, products, concatenations, or even objects/arrays

Syntax:

```js id="reduce1"
const result = array.reduce((accumulator, currentValue, index, array) => {
  // return updated accumulator
}, initialValue);
```

* `accumulator` → stores the accumulated value
* `currentValue` → current element being processed
* `index` → current index (optional)
* `array` → the original array (optional)
* `initialValue` → starting value for accumulator

---

## 2. Basic Example: Sum of Numbers

```js id="reduce2"
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // 15
```

* Starts with `0` and adds each number

---

## 3. Product of Numbers

```js id="reduce3"
const numbers = [1, 2, 3, 4];
const product = numbers.reduce((acc, curr) => acc * curr, 1);

console.log(product); // 24
```

---

## 4. Reduce to Object

```js id="reduce4"
const users = [
  { name: "Howard", age: 21 },
  { name: "Alice", age: 25 },
];

const userAges = users.reduce((acc, user) => {
  acc[user.name] = user.age;
  return acc;
}, {});

console.log(userAges);
// { Howard: 21, Alice: 25 }
```

* Can convert arrays into objects

---

## 5. React Example: Summing Values

```jsx id="reduce5"
const cart = [
  { item: "Laptop", price: 50000 },
  { item: "Mouse", price: 500 },
];

const total = cart.reduce((acc, product) => acc + product.price, 0);

console.log(total); // 50500
```

* Useful for **calculating totals in React apps**

---

## 6. Reduce for Array Flattening

```js id="reduce6"
const nested = [[1, 2], [3, 4], [5]];
const flat = nested.reduce((acc, arr) => acc.concat(arr), []);

console.log(flat); // [1, 2, 3, 4, 5]
```

* Flattens arrays of arrays into a single array

---

## 7. Common Mistakes

* Forgetting `initialValue`

```js id="reduce7"
// ❌ Wrong
const numbers = [];
const sum = numbers.reduce((a, b) => a + b);
// Throws error because array is empty

// ✅ Correct
const sumCorrect = numbers.reduce((a, b) => a + b, 0); // 0
```

* Returning `undefined` instead of `accumulator`

```js id="reduce8"
// ❌ Wrong
numbers.reduce((acc, curr) => { acc + curr }); // returns undefined

// ✅ Correct
numbers.reduce((acc, curr) => { return acc + curr; }, 0);
```

---

## 8. Practice

```js id="reduce9"
const numbers = [2, 3, 4];

// Use reduce to calculate sum
```

Answer:

```js id="reduce10"
const sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 9
```

---

## 9. Summary

* `reduce()` **reduces an array to a single value**
* Can return a **number, string, object, or array**
* Must **return accumulator** in each step
* Powerful for **calculations and transformations** in React

---

## Rule

Use `reduce()` when you want to **combine array elements into a single value**, like sums, totals, objects, or flattened arrays.
