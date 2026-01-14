# useContext Hook

## Overview
`useContext` is a React Hook that lets you read and subscribe to context from your component. It provides a way to pass data through the component tree without having to pass props down manually at every level.

## Basic Syntax
```javascript
const value = useContext(SomeContext);
```

## How It Works

1. Create Context
```javascript
// Create a context (usually in a separate file)
import { createContext } from 'react';

const LanguageContext = createContext({
  language: 'en',
  setLanguage: () => {}
});

export default LanguageContext;
```
2. Provide Context Value

```javascript

function App() {
  const [language, setLanguage] = useState('en');
  
  return (
    <LanguageContext.Provider value={{ language, setLanguage }}>
      <Header />
      <MainContent />
      <Footer />
    </LanguageContext.Provider>
  );
}
```

3. Consume Context

``` javascript
// Any child component can access context
function Header() {
  const { language } = useContext(LanguageContext);
  
  return (
    <header>
      Current language: {language}
    </header>
  );

// current language should show as en
}
```