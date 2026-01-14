# Type Aliases and Index Signatures

## Index Signatures

### Pattern: `{ [index: string]: Type }`
```typescript
// Object with dynamic string keys, all values of same type
type StringDictionary = { [key: string]: string };
type MetricMap = { [metricName: string]: Metric };

// Your example:
type GroupBreakdown = { [index: string]: GroupMetric };
// Means: "An object where any string key maps to a GroupMetric"

// 1. API responses with dynamic keys
type ApiResponse = { [endpoint: string]: any };

// 2. Component props with dynamic attributes
type DynamicProps = { [propName: string]: string | number };

// 3. Translation dictionaries  
type Translations = { [key: string]: string };

// 4. Configuration objects
type Config = { [setting: string]: boolean | number | string };
```

## Type Aliases vs Interfaces

### Type Alias

```typescript
// For object types, unions, intersections, primitives
type GroupBreakdown = { [key: string]: GroupMetric };
type UserID = string | number;
type ApiResponse<T> = { data: T; status: number };
```
### Interface

```typescript
// Primarily for object shapes, can be extended
interface GroupBreakdown {
  [key: string]: GroupMetric;
}
interface ApiResponse<T> {
  data: T;
  status: number;
}
``` 
### Real-World Example: Your Function

```typescript

export type GroupBreakdown = { [index: string]: GroupMetric };

export const groupBreakdownFor = (
  query: Query, 
  report: MetricReport
): Promise<GroupBreakdown> => {
  return request(`group-breakdown/${report}`, {
    method: "POST",
    body: JSON.stringify({ query }),
  })
  .then(res => res.json())
  .then(result => result.data);
};

// Key concepts:
// 1. Index signature for flexible key names
// 2. Promise return type for async operations
// 3. Type-safe parameters (Query, MetricReport)
// 4. Promise chain with type inference
```