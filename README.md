# JavaScript Essentials for React

A comprehensive guide to essential JavaScript concepts and patterns for React development. This repository covers modern JavaScript features that are fundamental to writing clean, idiomatic React code.

---

## 📚 Table of Contents

### Core Concepts

1. **[Variables: `const` and `let`](#1-variables-const-and-let)** – Variable declaration patterns
2. **[Destructuring](#2-destructuring)** – Object and array destructuring
3. **[Rest and Spread Operators](#3-rest-and-spread-operators)** – Expanding and collecting values
4. **[Template Literals](#4-template-literals)** – String interpolation and formatting
5. **[Ternary Operators](#5-ternary-operators-vs-ifelse)** – Concise conditional expressions
6. **[Arrow Functions](#6-arrow-functions)** – Modern function syntax

### Operators & Logic

7. **[Short-Circuiting and Logical Operators](#7-short-circuiting-and-logical-operators)** – `&&`, `||`, and `??`
8. **[Optional Chaining](#8-optional-chaining)** – Safe property access with `?.`

### Array Methods

9. **[Map Method](#9-map-method)** – Transform array elements
10. **[Filter Method](#10-filter-method)** – Select array elements
11. **[Reduce Method](#11-reduce-method)** – Aggregate array values
12. **[Sort Method](#12-array-sort-method)** – Order array elements

### Data Handling

13. **[Working with Immutable Arrays](#13-working-with-immutable-arrays)** – React-safe array operations

### Asynchronous Programming

14. **[Promises](#14-asynchronous-promises)** – Promise-based async operations
15. **[Async/Await](#15-asynchronous-asyncawait)** – Modern async syntax

---

## 1. Variables: `const` and `let`

### Golden Rule

- Use `const` by default
- Use `let` if the value will change

```js
const name = "Howard";

let count = 0;
count++;
```

### Beginner Pattern

Start with `const`:

```js
const price = 100;
```

Switch to `let` only when needed:

```js
let total = 0;
total += 10;
```

### React Basic Pattern

Components use `const`:

```jsx
const App = () => {
  return <h1>Hello React</h1>;
};
```

Props also use `const`:

```jsx
const Welcome = ({ name }) => {
  return <h1>Hello {name}</h1>;
};
```

### Avoid Mutation

Do not change arrays or objects directly.

**Bad:**

```js
const arr = [1, 2];
arr.push(3);
```

**Good:**

```js
const arr = [1, 2];
const newArr = [...arr, 3];
```

### Loop Pattern

Use `let` when values change in loops:

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### Conditional Pattern

Use `let` when value depends on logic:

```js
let result;

if (score > 50) {
  result = "Pass";
} else {
  result = "Fail";
}
```

---

## 2. Destructuring

### Overview

Destructuring is a way to **extract values from objects and arrays**.

**Benefits:**

- Shorter code
- Cleaner syntax
- Easier to read and maintain

### Object Destructuring

#### Basic Example

```js
const user = {
  name: "Howard",
  age: 21,
};

const { name, age } = user;

console.log(name); // Howard
console.log(age); // 21
```

#### Renaming Variables

```js
const user = { name: "Howard" };

const { name: username } = user;

console.log(username); // Howard
```

#### Default Values

```js
const user = { name: "Howard" };

const { age = 18 } = user;

console.log(age); // 18
```

#### Nested Destructuring

```js
const user = {
  name: "Howard",
  address: { city: "Manila" },
};

const {
  address: { city },
} = user;

console.log(city); // Manila
```

#### Using Spread with Objects

```js
const user = { name: "Howard", age: 21, country: "PH" };

const { name, ...rest } = user;

console.log(name); // Howard
console.log(rest); // { age: 21, country: "PH" }
```

### Array Destructuring

#### Basic Example

```js
const fruits = ["apple", "banana", "mango"];

const [first, second] = fruits;

console.log(first); // apple
console.log(second); // banana
```

---

## 3. Rest and Spread Operators

### Overview

Rest (`...`) and Spread (`...`) look the same but have **different uses**:

- **Spread**: expands elements of arrays or properties of objects
- **Rest**: collects multiple elements into a single array or object

### Spread Operator (`...`)

#### Arrays

```js
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4, 5];

console.log(newNumbers); // [1, 2, 3, 4, 5]
```

- Expands elements of `numbers` into a new array
- Useful to **avoid mutating the original array**

#### Objects

```js
const user = { name: "Howard", age: 21 };
const updatedUser = { ...user, country: "PH" };

console.log(updatedUser);
// { name: "Howard", age: 21, country: "PH" }
```

- Copies all properties from `user` into a new object
- Can **add or override properties**

#### Function Arguments

```js
const nums = [1, 2, 3];

const sum = (a, b, c) => a + b + c;

console.log(sum(...nums)); // 6
```

- Expands array into individual arguments

### Rest Operator (`...`)

#### Arrays

```js
const [first, ...rest] = [1, 2, 3, 4];

console.log(first); // 1
console.log(rest); // [2, 3, 4]
```

- Collects the **remaining elements** into an array

#### Objects

```js
const { name, ...others } = { name: "Howard", age: 21, country: "PH" };

console.log(name); // Howard
console.log(others); // { age: 21, country: "PH" }
```

- Collects **remaining properties** into a new object

#### Function Parameters

```js
const sum = (...numbers) => {
  return numbers.reduce((acc, curr) => acc + curr, 0);
};

console.log(sum(1, 2, 3, 4)); // 10
```

- Collects **any number of arguments** into an array

---

## 4. Template Literals

### Overview

Template literals allow you to create **strings easily** and **embed variables** without using `+` for concatenation.

- Use **backticks** `` ` `` instead of quotes `' '` or `" "`
- Use **`${}`** to insert expressions

### Basic Example

```js
const name = "Howard";
const greeting = `Hello, ${name}!`;

console.log(greeting); // Hello, Howard!
```

### Multi-line Strings

```js
const message = `This is line 1
This is line 2
This is line 3`;

console.log(message);
/*
This is line 1
This is line 2
This is line 3
*/
```

No need for `\n` for line breaks.

### Expressions Inside Template Literals

```js
const a = 10;
const b = 20;

const result = `The sum of ${a} + ${b} is ${a + b}`;

console.log(result); // The sum of 10 + 20 is 30
```

### Template Literals with Functions

```js
const user = { name: "Howard", age: 21 };

const message = `Hello ${user.name}, you are ${user.age} years old.`;

console.log(message);
```

### Using Template Literals in React

```jsx
const name = "Howard";
const greeting = `Hello ${name}, welcome to React!`;

const App = () => <h1>{greeting}</h1>;
```

Makes **JSX expressions cleaner** and easier than concatenation with `+`.

### Tagged Template Literals (Advanced)

```js
function highlight(strings, ...values) {
  return strings.reduce(
    (result, str, i) =>
      `${result}<strong>${values[i - 1] || ""}</strong>${str}`,
  );
}

const name = "Howard";
const age = 21;

const message = highlight`My name is ${name} and I am ${age} years old.`;

console.log(message);
// My name is <strong>Howard</strong> and I am <strong>21</strong> years old.
```

---

## 5. Ternary Operators vs If/Else

### Overview

The **ternary operator** is a **shorter way to write simple if/else statements**.

**Syntax:**

```js
condition ? valueIfTrue : valueIfFalse;
```

- `condition` → expression that evaluates to `true` or `false`
- `valueIfTrue` → returned if condition is true
- `valueIfFalse` → returned if condition is false

### Basic Example

```js
const age = 18;
const canVote = age >= 18 ? "Yes" : "No";

console.log(canVote); // Yes
```

- `age >= 18` → condition
- `"Yes"` → if true
- `"No"` → if false

### Replacing Simple if/else

**Instead of:**

```js
let status;
if (age >= 18) {
  status = "Adult";
} else {
  status = "Minor";
}
```

**You can write:**

```js
const status = age >= 18 ? "Adult" : "Minor";
```

- Cleaner and shorter
- Works for simple conditions

### Nested Ternaries (Advanced)

```js
const score = 85;
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";

console.log(grade); // B
```

- Can replace multiple if/else statements
- Be careful: **don't over-nest**, it reduces readability

### React Examples

#### Conditional Rendering

```jsx
const isLoggedIn = true;

const App = () => (
  <div>{isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please log in</h1>}</div>
);
```

- Ternary operators are **commonly used in JSX**
- Keeps rendering logic compact

#### Inline Class Names

```jsx
const isActive = false;

const buttonClass = `btn ${isActive ? "btn-active" : "btn-inactive"}`;

console.log(buttonClass); // "btn btn-inactive"
```

---

## 6. Arrow Functions

### Overview

Arrow functions provide a **shorter syntax** for writing functions and handle the `this` keyword differently from regular functions.

**Syntax:**

```js
const functionName = (parameters) => {
  // function body
};
```

- Use `()` for parameters
- Use `{}` for multiple statements
- If single expression, `{}` and `return` can be omitted

### Basic Examples

#### Single-line arrow function

```js
const add = (a, b) => a + b;

console.log(add(2, 3)); // 5
```

- Single expression → returns automatically

#### Multiple-line arrow function

```js
const multiply = (a, b) => {
  const result = a * b;
  return result;
};

console.log(multiply(2, 3)); // 6
```

- Use `{}` and `return` for multiple statements

#### No parameters

```js
const greet = () => "Hello World";

console.log(greet()); // Hello World
```

#### Single parameter (no parentheses needed)

```js
const square = (x) => x * x;

console.log(square(4)); // 16
```

### Arrow Functions in React

#### Functional Components

```jsx
const App = () => <h1>Hello React</h1>;
```

- Always use `const` + arrow function for components

#### Event Handlers

```jsx
const Button = () => {
  const handleClick = () => console.log("Clicked!");

  return <button onClick={handleClick}>Click me</button>;
};
```

- Arrow functions keep **`this` context** predictable

#### Map Function

```jsx
const users = [
  { id: 1, name: "Howard" },
  { id: 2, name: "Alice" },
];

const UserList = () => (
  <ul>
    {users.map((user) => (
      <li key={user.id}>{user.name}</li>
    ))}
  </ul>
);
```

---

## 7. Short-Circuiting and Logical Operators

### Overview

Logical operators can be used not only for **true/false checks** but also for **short-circuit evaluation**.

- **`&&`** → returns right-hand side if left-hand side is truthy
- **`||`** → returns left-hand side if truthy, otherwise right-hand side
- **`??`** → nullish coalescing, returns right-hand side if left-hand side is `null` or `undefined`

### AND (`&&`) Operator

```js
const isLoggedIn = true;
const message = isLoggedIn && "Welcome back!";

console.log(message); // "Welcome back!"
```

- If `isLoggedIn` is `true` → returns right-hand value
- If `isLoggedIn` is `false` → returns `false`

#### React Example

```jsx
const isLoggedIn = true;

const App = () => <div>{isLoggedIn && <h1>Welcome back!</h1>}</div>;
```

- Common pattern for **conditional rendering**

### OR (`||`) Operator

```js
const username = "";
const defaultName = username || "Guest";

console.log(defaultName); // "Guest"
```

- Returns **first truthy value**
- Useful for **default values**

#### React Example

```jsx
const user = { name: "" };

const App = () => <h1>Hello {user.name || "Guest"}</h1>;
```

### Nullish Coalescing (`??`) Operator

```js
const count = 0;
const displayCount = count ?? 10;

console.log(displayCount); // 0
```

- Only returns right-hand side if **left-hand side is `null` or `undefined`**
- Different from `||` because `0`, `""`, `false` are considered valid

#### React Example

```jsx
const user = { name: null };

const App = () => <h1>Hello {user.name ?? "Guest"}</h1>;
```

### Combining Operators

```js
const isLoggedIn = true;
const username = "";

const displayName = isLoggedIn && (username || "Guest");

console.log(displayName); // "Guest"
```

- Use `&&` to check conditions
- Use `||` or `??` for default values

---

## 8. Optional Chaining

### Overview

Optional chaining allows you to **safely access nested object properties** without worrying about `undefined` or `null`.

- Syntax: `object?.property`
- Stops evaluation if the value before `?.` is `null` or `undefined`
- Prevents runtime errors

### Basic Example

```js
const user = { name: "Howard" };

console.log(user?.name); // "Howard"
console.log(user?.age); // undefined (instead of error)
```

### Nested Properties

```js
const user = {
  name: "Howard",
  address: { city: "Manila" },
};

console.log(user?.address?.city); // "Manila"
console.log(user?.address?.zip); // undefined
```

- Each `?.` checks if the previous value exists before accessing the next property

### Optional Chaining with Arrays

```js
const users = [{ name: "Howard" }];

console.log(users?.[0]?.name); // "Howard"
console.log(users?.[1]?.name); // undefined
```

- Use `?.[index]` for arrays

### Optional Chaining with Functions

```js
const user = {
  greet: () => "Hello!",
};

console.log(user.greet?.()); // "Hello!"
console.log(user.sayHi?.()); // undefined
```

- Use `?.()` to safely call a function that might not exist

### React Examples

#### Accessing Props Safely

```jsx
const UserProfile = ({ user }) => <h1>{user?.name ?? "Guest"}</h1>;
```

- Prevents errors if `user` is `undefined`
- Works well with default values using `??`

#### Accessing Nested State

```jsx
const [data, setData] = useState(null);

console.log(data?.user?.name); // undefined if data is null
```

- Avoids runtime crashes when state is initially `null`

### Common Mistakes

- Forgetting to use `?.` before deeply nested properties

```js
// Throws error if user is null
console.log(user?.address.city); // ❌ May crash if address is null
console.log(user?.address?.city); // ✅ Safe
```

---

## 9. Map Method

### Overview

The `map()` method **creates a new array** by applying a function to each element of an existing array.

- Original array **is not modified**
- Very common in React for **rendering lists**

**Syntax:**

```js
const newArray = array.map((element, index) => {
  // return new value
});
```

- `element` → current item
- `index` → current item's position (optional)
- Function returns the **new element**

### Basic Example

```js
const numbers = [1, 2, 3];
const doubled = numbers.map((n) => n * 2);

console.log(doubled); // [2, 4, 6]
```

- Original `numbers` array stays `[1, 2, 3]`

### Using Index

```js
const fruits = ["apple", "banana", "mango"];
const fruitList = fruits.map((fruit, i) => `${i + 1}. ${fruit}`);

console.log(fruitList);
// ["1. apple", "2. banana", "3. mango"]
```

- Index is useful for **numbering** or as **React keys**

### Objects in Array

```js
const users = [
  { name: "Howard", age: 21 },
  { name: "Alice", age: 25 },
];

const names = users.map((user) => user.name);

console.log(names); // ["Howard", "Alice"]
```

- Extract specific properties from objects

### React Example: Rendering Lists

```jsx
const users = [
  { id: 1, name: "Howard" },
  { id: 2, name: "Alice" },
];

const UserList = () => (
  <ul>
    {users.map((user) => (
      <li key={user.id}>{user.name}</li>
    ))}
  </ul>
);
```

- Always provide a **unique `key`** for list items in React

### Chaining with Other Methods

```js
const numbers = [1, 2, 3, 4, 5];

const doubledEven = numbers.filter((n) => n % 2 === 0).map((n) => n * 2);

console.log(doubledEven); // [4, 8]
```

---

## 10. Filter Method

### Overview

The `filter()` method **creates a new array** with elements that pass a test defined by a function.

- Original array **is not modified**
- Returns **only elements that satisfy the condition**

**Syntax:**

```js
const newArray = array.filter((element, index) => {
  // return true to keep element
});
```

- `element` → current item
- `index` → current item's position (optional)
- Return **true** to keep, **false** to discard

### Basic Example

```js
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((n) => n % 2 === 0);

console.log(evenNumbers); // [2, 4]
```

- Keeps only **even numbers**

### Filtering Objects

```js
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

### React Example: Conditional Rendering

```jsx
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

### Using Index

```js
const fruits = ["apple", "banana", "mango"];

const firstTwo = fruits.filter((_, index) => index < 2);

console.log(firstTwo); // ["apple", "banana"]
```

- Index can help **limit results**

### Combining with Other Methods

```js
const numbers = [1, 2, 3, 4, 5, 6];

const doubledEven = numbers.filter((n) => n % 2 === 0).map((n) => n * 2);

console.log(doubledEven); // [4, 8, 12]
```

---

## 11. Reduce Method

### Overview

The `reduce()` method **reduces an array to a single value** by applying a function to each element in the array.

- Original array **is not modified**
- Can calculate sums, products, concatenations, or even objects/arrays

**Syntax:**

```js
const result = array.reduce((accumulator, currentValue, index, array) => {
  // return updated accumulator
}, initialValue);
```

- `accumulator` → stores the accumulated value
- `currentValue` → current element being processed
- `index` → current index (optional)
- `array` → the original array (optional)
- `initialValue` → starting value for accumulator

### Basic Example: Sum of Numbers

```js
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // 15
```

- Starts with `0` and adds each number

### Product of Numbers

```js
const numbers = [1, 2, 3, 4];
const product = numbers.reduce((acc, curr) => acc * curr, 1);

console.log(product); // 24
```

### Reduce to Object

```js
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

- Can convert arrays into objects

### React Example: Summing Values

```jsx
const cart = [
  { item: "Laptop", price: 50000 },
  { item: "Mouse", price: 500 },
];

const total = cart.reduce((acc, product) => acc + product.price, 0);

console.log(total); // 50500
```

- Useful for **calculating totals in React apps**

### Reduce for Array Flattening

```js
const nested = [[1, 2], [3, 4], [5]];
const flat = nested.reduce((acc, arr) => acc.concat(arr), []);

console.log(flat); // [1, 2, 3, 4, 5]
```

- Flattens arrays of arrays into a single array

---

## 12. Array Sort Method

### Overview

The `sort()` method **sorts the elements of an array in place** and **returns the sorted array**.

- Default sort is **lexicographical** (like strings)
- Can provide a **compare function** for numeric or custom sorting
- **Original array is modified**

**Syntax:**

```js
array.sort((a, b) => {
  // return < 0 → a before b
  // return 0 → keep order
  // return > 0 → b before a
});
```

### Sorting Strings

```js
const fruits = ["banana", "apple", "mango"];
fruits.sort();

console.log(fruits); // ["apple", "banana", "mango"]
```

- Default sort works well for **strings**

### Sorting Numbers

```js
const numbers = [10, 5, 20, 1];
numbers.sort();

console.log(numbers); // [1, 10, 20, 5] ❌ unexpected
```

- Default sort treats numbers as strings → **not numeric**

#### Correct Numeric Sort

```js
const numbers = [10, 5, 20, 1];
numbers.sort((a, b) => a - b);

console.log(numbers); // [1, 5, 10, 20]
```

- `a - b` → ascending
- `b - a` → descending

### Sorting Objects

```js
const users = [
  { name: "Howard", age: 21 },
  { name: "Alice", age: 25 },
  { name: "Bob", age: 18 },
];

users.sort((a, b) => a.age - b.age);

console.log(users);
// [{ name: "Bob", age: 18 }, { name: "Howard", age: 21 }, { name: "Alice", age: 25 }]
```

- Sort by **object property** using a compare function

### React Example: Rendering Sorted List

```jsx
const users = [
  { id: 1, name: "Howard", age: 21 },
  { id: 2, name: "Alice", age: 25 },
];

const UserList = () => (
  <ul>
    {users
      .sort((a, b) => a.name.localeCompare(b.name))
      .map((user) => (
        <li key={user.id}>{user.name}</li>
      ))}
  </ul>
);
```

---

## 13. Working with Immutable Arrays

### Overview

In React, **immutability is important**.

- Avoid modifying the original array directly
- Use **methods that return a new array** instead of mutating the old one

**Common mutable methods:** `push`, `pop`, `splice`, `sort`

**Common immutable methods:** `map`, `filter`, `reduce`, `concat`, `slice`, `spread (...)`

### Why Immutability Matters

```js
const numbers = [1, 2, 3];
const doubled = numbers.map((n) => n * 2);

console.log(numbers); // [1, 2, 3]  original not changed
console.log(doubled); // [2, 4, 6]
```

- React relies on **state changes**
- If you mutate the array, React may **not detect changes**

### Adding Items (Immutable)

```js
const fruits = ["apple", "banana"];

// Using spread
const newFruits = [...fruits, "mango"];
console.log(newFruits); // ["apple", "banana", "mango"]
```

- Original `fruits` array **not changed**

### Removing Items (Immutable)

```js
const numbers = [1, 2, 3, 4];

// Remove number 2
const newNumbers = numbers.filter((n) => n !== 2);
console.log(newNumbers); // [1, 3, 4]
```

- Use `filter()` to remove items **without mutating**

### Updating Items (Immutable)

```js
const users = [
  { id: 1, name: "Howard" },
  { id: 2, name: "Alice" },
];

// Change name of user with id 2
const updatedUsers = users.map((user) =>
  user.id === 2 ? { ...user, name: "Alicia" } : user,
);

console.log(updatedUsers);
// [{ id: 1, name: "Howard" }, { id: 2, name: "Alicia" }]
```

- Use `map()` + **spread** to update objects immutably

### React State Example

```jsx
const [tasks, setTasks] = useState(["Task 1", "Task 2"]);

const addTask = (task) => setTasks([...tasks, task]);
const removeTask = (task) => setTasks(tasks.filter((t) => t !== task));
```

- Always create **new array** when updating state
- Avoid `tasks.push()` or `tasks.splice()`

### Common Mistakes

Avoid using `push`, `splice`, or `sort` directly on **state arrays**:

```js
// Wrong: Mutates state directly
tasks.push("New Task");
setTasks(tasks);

// Correct: Creates new array
setTasks([...tasks, "New Task"]);
```

---

## 14. Asynchronous Promises

### Overview

A **Promise** is an object representing the **eventual completion or failure** of an asynchronous operation.

- Helps avoid **callback hell**
- Can be in **three states**:
  1. **Pending** – initial state
  2. **Fulfilled** – operation succeeded
  3. **Rejected** – operation failed

**Syntax:**

```js
const promise = new Promise((resolve, reject) => {
  // asynchronous code
});
```

- `resolve(value)` → marks promise as fulfilled
- `reject(error)` → marks promise as rejected

### Basic Example

```js
const fetchData = new Promise((resolve, reject) => {
  const success = true;

  setTimeout(() => {
    if (success) resolve("Data received!");
    else reject("Error occurred!");
  }, 1000);
});

fetchData
  .then((data) => console.log(data)) // "Data received!"
  .catch((error) => console.error(error));
```

- `then()` → handles **fulfilled**
- `catch()` → handles **rejected**

### Promises in React (Async Functions)

```js
const fetchUser = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve({ name: "Howard", age: 21 }), 1000);
  });
};

fetchUser().then((user) => console.log(user.name)); // Howard
```

- Promises often used with **API calls**

### Chaining Promises

```js
const fetchNumber = () => Promise.resolve(5);

fetchNumber()
  .then((num) => num * 2)
  .then((result) => console.log(result)); // 10
```

- Each `then()` receives the value returned from previous step

### Promise.all

```js
const promise1 = Promise.resolve(1);
const promise2 = Promise.resolve(2);
const promise3 = Promise.resolve(3);

Promise.all([promise1, promise2, promise3]).then((values) =>
  console.log(values),
); // [1, 2, 3]
```

- Waits for **all promises to resolve**
- Rejects if **any promise fails**

### Async/Await (Syntactic Sugar)

```js
const fetchData = () => Promise.resolve("Data loaded!");

const getData = async () => {
  const data = await fetchData();
  console.log(data);
};

getData();
```

---

## 15. Asynchronous: Async/Await

### Overview

`async`/`await` is **syntactic sugar for Promises**.

- Makes asynchronous code **look and behave like synchronous code**
- Helps avoid **callback hell** and messy `.then()` chains

### Basic Syntax

```js
const fetchData = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve("Data loaded!"), 1000);
  });
};

const getData = async () => {
  const data = await fetchData();
  console.log(data); // "Data loaded!"
};

getData();
```

- `async` → marks a function as asynchronous
- `await` → pauses execution until promise resolves

### Handling Errors

```js
const fetchData = () => Promise.reject("Error occurred!");

const getData = async () => {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error(error); // "Error occurred!"
  }
};

getData();
```

- Always use **try/catch** to handle rejected promises

### Returning Values from Async Functions

```js
const fetchNumber = async () => 10;

fetchNumber().then((result) => console.log(result)); // 10
```

- `async` functions always return a **Promise**
- `return` value is **wrapped in a promise**

### Multiple Async Calls

```js
const fetchUser = () => Promise.resolve({ name: "Howard" });
const fetchPosts = () => Promise.resolve(["Post 1", "Post 2"]);

const getData = async () => {
  const user = await fetchUser();
  const posts = await fetchPosts();
  console.log(user, posts);
};

getData();
```

- Sequential execution → **one after another**

#### Parallel Execution

```js
const getData = async () => {
  const [user, posts] = await Promise.all([fetchUser(), fetchPosts()]);
  console.log(user, posts);
};

getData();
```

- `Promise.all()` → **run multiple async tasks in parallel**

---

## 🎯 Quick Reference

### Essential Patterns for React

| Concept       | Pattern                          | Use Case                         |
| ------------- | -------------------------------- | -------------------------------- |
| Variables     | `const` first, `let` if needed   | Always follow this pattern       |
| Destructuring | `const { x, y } = obj`           | Simplify variable extraction     |
| Spread        | `[...arr, item]`                 | Immutable array operations       |
| Templates     | `` `Hello ${name}` ``            | String interpolation             |
| Ternary       | `condition ? true : false`       | Simple conditionals in JSX       |
| Arrow         | `() => JSX`                      | React components & handlers      |
| Map           | `arr.map(item => ...)`           | Render lists in React            |
| Filter        | `arr.filter(item => ...)`        | Conditional rendering            |
| Reduce        | `arr.reduce((acc, curr) => ...)` | Calculate totals, aggregate data |
| Optional      | `obj?.prop?.nested`              | Safe nested access               |
| Async         | `async () => { await ... }`      | Handle API calls                 |

---

## 📝 Notes

- **Immutability is key**: Always create new arrays/objects instead of mutating
- **React performance**: Use proper keys when rendering lists
- **Error handling**: Always use try/catch with async/await
- **Readability**: Don't over-nest ternaries or chains

---

## 🚀 Getting Started

Choose any topic and dive in! Each section includes:

- **Overview** of the concept
- **Basic examples** with explanations
- **React-specific patterns**
- **Common mistakes** to avoid

Start with Variables and work your way through to Async/Await for a comprehensive understanding of modern JavaScript for React!

---

**Happy Learning! 🎉**
