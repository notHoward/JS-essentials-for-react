# Optional Chaining (`?.`)

---

## 1. Overview

Optional chaining allows you to **safely access nested object properties** without worrying about `undefined` or `null`.

- Syntax: `object?.property`
- Stops evaluation if the value before `?.` is `null` or `undefined`
- Prevents runtime errors

---

## 2. Basic Example

```js id="oc1"
const user = { name: "Howard" };

console.log(user?.name); // "Howard"
console.log(user?.age); // undefined (instead of error)
```

---

## 3. Nested Properties

```js id="oc2"
const user = {
  name: "Howard",
  address: { city: "Manila" },
};

console.log(user?.address?.city); // "Manila"
console.log(user?.address?.zip); // undefined
```

- Each `?.` checks if the previous value exists before accessing the next property

---

## 4. Optional Chaining with Arrays

```js id="oc3"
const users = [{ name: "Howard" }];

console.log(users?.[0]?.name); // "Howard"
console.log(users?.[1]?.name); // undefined
```

- Use `?.[index]` for arrays

---

## 5. Optional Chaining with Functions

```js id="oc4"
const user = {
  greet: () => "Hello!",
};

console.log(user.greet?.()); // "Hello!"
console.log(user.sayHi?.()); // undefined
```

- Use `?.()` to safely call a function that might not exist

---

## 6. React Examples

### 6.1 Accessing Props Safely

```jsx id="oc5"
const UserProfile = ({ user }) => <h1>{user?.name ?? "Guest"}</h1>;
```

- Prevents errors if `user` is `undefined`
- Works well with default values using `??`

---

### 6.2 Accessing Nested State

```jsx id="oc6"
const [data, setData] = useState(null);

console.log(data?.user?.name); // undefined if data is null
```

- Avoids runtime crashes when state is initially `null`

---

## 7. Common Mistakes

- Forgetting to use `?.` before deeply nested properties

```js id="oc7"
//  Throws error if user is null
console.log(user.address.city);

//  Safe
console.log(user?.address?.city);
```

- Mixing optional chaining with nullish coalescing improperly

```js id="oc8"
const name = user?.name ?? "Guest"; //  Correct
const nameWrong = (user?.name ?? "Guest").length; //  Throws if user is null
```

---

## 8. Practice

```js id="oc9"
const user = { address: { city: "Manila" } };

// Safely log user's zip code
```

Answer:

```js id="oc10"
console.log(user?.address?.zip); // undefined
```

---

## 9. Summary

- Optional chaining: `?.`
- Safely access **nested properties, arrays, or functions**
- Returns `undefined` if any step is `null` or `undefined`
- Works perfectly with React props and state

---

## Rule

Use **optional chaining** to **prevent errors** when accessing values that might not exist instead of manually checking with `if` statements.
