# Array Methods

## find() Method
Returns the first element that satisfies the condition.

```javascript
const array = [
  { id: 1, name: "Alice" },
  { id: 2, name: "Bob" },
  { id: 3, name: "Charlie" }
];

// Find object where id is 2
const result = array.find(item => item.id === 2);
// { id: 2, name: "Bob" }

// Returns undefined if not found
const notFound = array.find(item => item.id === 99);
// undefined

// Common pattern with fallback
const item = array.find(x => x.id === 2) || { name: "Default" };
```

## Array `.map()` Method

### Overview
The `.map()` method creates a **new array** by calling a function on every element of the original array.

### Basic Syntax
```javascript
const newArray = array.map((currentValue, index, array) => {
  // return transformed element
});
```

