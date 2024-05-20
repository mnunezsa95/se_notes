See [[React - Introduction to React.js]]
Resources:
* [Common Mistakes When Using React useState Hook (With Code Examples)](https://hashnode.com/@AkshayKaushik)

---
#### `useState()`
* A hook in React.js used to manage state (completely overwrites state)
* Returns an array with two elements
	* the current state value
	* the setter function
```jsx
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

return (
  <div>
    <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### Common mistakes when using `useState()`
1. Forgetting to handle arrays and objects correctly
	* Since the `tags` array was mutated directly, React can't detect changes and won't trigger re-renders properly.
```jsx
const [tags, setTags] = useState(['react', 'javascript']);
const addTag = () => { 
  tags.push('nodejs'); // Mutates existing array  
}
return <div>{tags}</div>
```

```jsx
// Instead, create a new copy of array/object before passing to setter fn
const addTag = () => {
  setTags([...tags, 'nodejs']);  
}
```

2. Making unnecessary `useState()` calls
	* There's no need to separate every single field or data point into its own state hook.
```jsx
function MyForm() {
  const [firstName, setFirstName] = useState(''); 
  const [lastName, setLastName] = useState('');
  return (
    <>
      <input 
        value={firstName}
        onChange={(e) => setFirstName(e.target.value)}
      />
      <input
        value={lastName}  
        onChange={(e) => setLastName(e.target.value)} 
      />
    </>
  );
}
```

```jsx
// Instead, group related state into single objects:
function MyForm() {
  const [fields, setFields] = useState({
    firstName: '',
    lastName: '' 
  })

  // Call once to update both name fields
  const handleChange = (e) => {
    setFields({
      ...fields,
      [e.target.name]: e.target.value 
    })
  }
...
}
```

3. Incorrect State Comparison
	* When dealing with objects or arrays, avoid direct comparisons for state changes.
```jsx
// Incorrect
if (user !== newUser) {
  // ...
}

// Correct
if (user.id !== newUser.id) {
  // ...
}
```

4. Not Setting Proper Initial State

-Initialize based on props
* Use props instead of hard-values
```jsx
// Hard-coded [AVOID]
const [count, setCount] = useState(0); 

// Initialise based on props
const [count, setCount] = useState(props.initialCount);
```

-Handle unloaded data
* If fetching data in `useEffect`, set loading state
```jsx
const [user, setUser] = useState(null);

useEffect(() => {
  fetchUser().then(user => setUser(user))  
}, []);

// Check for null before rendering
return <div>{user ? user.name : 'Loading...'}</div>
```

-Specify data types for state
* Typing state helps avoid issues
```jsx
const [count, setCount] = useState<number>(0);
const [user, setUser] = useState<{name: string} | null>(null);
```