## Dynamic Property Access

### Using Template Literals for Property Names
```javascript
// Dynamic property access with template literals
const language = "es";
const obj = {
  dashboardNotes: "English notes",
  es_dashboardNotes: "Spanish notes"
};

// Access property dynamically
const propertyName = `${language}_dashboardNotes`;
console.log(obj[propertyName]); // "Spanish notes"
```
## Nested Dynamic Property Access

### Chained Bracket Notation
```javascript
// Two-step property lookup
const value = object1[object2[key]];

// Breakdown:
// 1. object2[key] - Gets a value from object2 using key
// 2. object1[result] - Uses that result as key to access object1

// Practical example: Translation mapping
const idMap = { 
  home: "page.home", 
  about: "page.about" 
};
const translations = { 
  "page.home": "Home Page", 
  "page.about": "About Us" 
};

const key = "home";
const displayText = translations[idMap[key]]; 
// idMap["home"] = "page.home"
// translations["page.home"] = "Home Page"
```

## Object.keys() - Getting Property Names

### What It Does
Returns an **array of a given object's own enumerable property names** (keys).

```javascript
const user = {
  id: 1,
  name: "John",
  email: "john@example.com"
};

const keys = Object.keys(user);
// Result: ['id', 'name', 'email']
```