# BACKEND, TYPESCRIPT AND EMAIL APIS THROUGH DESTRUCTURING

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


# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse
