See [[React - Introduction to React.js]], [[React.js - Higher Order Components]]
Resources:
* [10 Expert Performance Tips Every Senior JS React Developer Should Know](https://medium.com/@khushi1399gupta/10-expert-performance-tips-every-senior-js-react-developer-should-know-a786fc13f5c7)
*  [Dynamic Imports in React](https://medium.com/@shubham3480/dynamic-imports-in-react-3e3e7ad1d210)

---

#### What is `React.lazy()`?
* `React.lazy()` is a higher-order component that allows for us to “lazy-load” just the things that are currently needed by the user
* `React.lazy()` makes a call to a dynamic import and returns a promise

#### What is `React.Suspense`?
* `React.Suspense` allows for conditionally suspending the rendering of a React component until it is loaded
* `React.Suspense` provides a fallback prop that accepts a React element which either is a JSX snippet or a React component.

#### Why use `React.lazy()` and `React.Suspense`
* Can dramatically improve the performance of your app by only rendering what the user needs
* Prevents users from experiencing a blank page as a result of slow internet connection

#### Example: Using `React.lazy()` and `React.Suspense`
* The lazy component needs to be wrapped inside `<Suspense />` component
* `<Suspense/>` has a fallback prop to show something else while loading
```JSX
import React, { Suspense } from 'react';  

const MyLazyComponent = React.lazy(() => import('./MyLazyComponent'));

function App() {  
  return (  
    <div>  
      <Suspense fallback={<div>Loading...</div>}>  
        <MyLazyComponent />  
      </Suspense>  
    </div>  
  );  
}

export default App;
```
