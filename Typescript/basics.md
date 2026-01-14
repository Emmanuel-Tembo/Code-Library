## TypeScript in Functions

### Function with Type Annotation
```typescript
// Parameter type annotation
const getGuidanceStr = (actualTitle: string) => {
  // function body
};

// Explicit return type (optional but recommended)
const getGuidanceStr = (actualTitle: string): string => {
  // Must return a string
};

// Type inference on variables
const currentMeasure = getMeasures().find(...); 
// TypeScript infers the type based on return value
