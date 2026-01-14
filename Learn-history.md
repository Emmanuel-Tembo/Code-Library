# My Learn history

## Today's Learnings - [Wed 07 Jan]

### Code Pattern: Dynamic Language Fallback
Found this pattern for handling multi-language content:

```typescript
const getGuidanceStr = (actualTitle: string) => {
  const currentMeasure = getMeasures().find(measure => measure.title == actualTitle) || { dashboardNotes: "" };
  
  if (language != "en" && !!currentMeasure[`${language}_dashboardNotes`]) {
    return currentMeasure[`${language}_dashboardNotes`];
  }
  
  return currentMeasure.dashboardNotes;
};