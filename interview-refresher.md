# Interview

- When do you chooose controlled & uncontrolled components
  - Single source of truth, visual feedback, instant validation for Controlled
  - Performance for Uncontrolled
- React Reconsilation & keys
  - Diff & update only what has changed between virtual DOM & real DOM
  - keys (not array indices but uIds)
- How to Prevent Rerenders?
  - Single responsibility Components
  - Dicriminated State lifting
  - Memo
- Pitfalls of useEffect
  - Missed dependency array
  - Missed effect cleanup
- When do you choose useReducer over useState
  - Multi step state update
  - Centralized logic to avoid unnecessary props drilling

```js
 import React, { useEffect, useReducer, useState } from 'react';

const App = () => {
  const reducer = (state, action) => {
    switch(action.type) {
      case "increment":
        return {...state, counter: state.counter + 1}
      default:
        return state;
    }
  }

 const [state, dispatch] = useReducer(reducer, {counter: 0, timer: 0});
 
 useEffect(() => {
   dispatch({type: "increment"});
 }, []);
 
  return (
   <h3>{JSON.stringify(state)}</h3>
  )
}

export default App

// output
// {"counter":1,"timer":0}
```

- Bundle optimization
- RTK vs React Query
  - client side state management
  - api side state management with caching, background fetching
- TypeScript & Code
  - Discriminated usage of Union
  - Reusable Generics
  - Interfaces for Components
- Accessibility (a11y)
  - HTML Semantics, roles
  - Baked in keyboard accessibility, WCAG
  - Contrast ratio
  - Testing with screen readers
- Complex form validation
  - Debounce
- Leadership
  - Paired Programming
  - Guided PR reviews
  - Architectutal Decision Records (ADR) & Best Practices Playbook
- Security
  - XSS - Sanitize input, escape response, avaoid dangerouslySetInnerHTML
  - CSRF
  - Clickjacking - CSP Policy :: X-FRAME-Options: SAMEORIGIN
