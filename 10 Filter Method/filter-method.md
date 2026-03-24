# The Array `filter()` Method

---

## 1. Overview

The `filter()` method **creates a new array** with elements that pass a test defined by a function.

- Original array **is not modified**
- Returns **only elements that satisfy the condition**

Syntax:

```js id="filter1"
const newArray = array.filter((element, index) => {
  // return true to keep element
});
```

- `element` → current item
- `index` → current item’s position (optional)
- Return **true** to keep, **false** to discard

---

## 2. Basic Example

```js id="filter2"
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((n) => n % 2 === 0);

console.log(evenNumbers); // [2, 4]
```

- Keeps only **even numbers**

---

## 3. Filtering Objects

```js id="filter3"
const users = [
  { name: "Howard", age: 21 },
  { name: "Alice", age: 25 },
  { name: "Bob", age: 17 },
];

const adults = users.filter((user) => user.age >= 18);

console.log(adults);
// [{ name: "Howard", age: 21 }, { name: "Alice", age: 25 }]
```

- Useful to **filter lists in React**

---

## 4. React Example: Conditional Rendering

```jsx id="filter4"
const users = [
  { id: 1, name: "Howard", active: true },
  { id: 2, name: "Alice", active: false },
];

const ActiveUsers = () => (
  <ul>
    {users
      .filter((user) => user.active)
      .map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
  </ul>
);
```

- Filter **active users** before rendering

---

## 5. Using Index

```js id="filter5"
const fruits = ["apple", "banana", "mango"];

const firstTwo = fruits.filter((_, index) => index < 2);

console.log(firstTwo); // ["apple", "banana"]
```

- Index can help **limit results**

---

## 6. Combining with Other Methods

```js id="filter6"
const numbers = [1, 2, 3, 4, 5, 6];

const doubledEven = numbers.filter((n) => n % 2 === 0).map((n) => n * 2);

console.log(doubledEven); // [4, 8, 12]
```

- Combine `filter()` with `map()` or `sort()`

---

## 7. Common Mistakes

- Forgetting to **return a boolean**

```js id="filter7"
//  Wrong
const numbers = [1, 2, 3];
const evens = numbers.filter((n) => n % 2); // keeps odd numbers by mistake

//  Correct
const evensCorrect = numbers.filter((n) => n % 2 === 0);
```

- Using `filter()` when you just need **one item** → use `find()` instead

---

## 8. Practice

```js id="filter8"
const numbers = [5, 10, 15, 20];

// Keep numbers greater than 10
```

Answer:

```js id="filter9"
const filtered = numbers.filter((n) => n > 10);
console.log(filtered); // [15, 20]
```

---

## 9. Summary

- `filter()` **creates a new array** based on a condition
- Does **not modify the original array**
- Works with numbers, strings, objects, arrays
- Common in React to **conditionally render lists**

---

## Rule

Use `filter()` when you need to **keep only elements that satisfy a condition**.
