# Ternery Operator: 

### Basic Syntax
```javascript
condition ? expressionIfTrue : expressionIfFalse
```

## Overview
The ternary (conditional) operator is the only JavaScript operator that takes three operands. It's a concise alternative to `if...else` statements.


# chaining

```typescript
    if (
      !confirmation.data?.data ||
      emailSent ||
      !confirmation.data.data.guestEmail
    )
    return;
```

1. This above snippet is a guard clause if any of the conditions:
- Condition 1 : check if teh confirmation data is missing null or undefined and the the optional chaining operator (?.) prevents a runtime crash if confirmastion.data is null
- condition 2: checks if emailSent is already true
- condition 3: 

## Logical Operators

### Double Bang (!!) - Boolean Conversion
```javascript
const value = "some text";
const isTruthy = !!value; // true

// Used to convert any value to boolean
!!null        // false
!!undefined   // false
!!0           // false
!!"hello"     // true
!![]          // true
!!{}          // true

// Practical use: checking if property exists and is truthy
if (!!obj[propertyName]) {
  // Property exists and has a truthy value
}