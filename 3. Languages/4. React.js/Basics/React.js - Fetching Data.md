See [[React - Introduction to React.js]]

---

#### Data Fetching using Hooks
* There are two popular hooks for fetching data 
	1) `useState()`
	2) `useEffect()`

#### Example: Fetching Data in React
1)  Import Dependencies
2) Initialize the State
3) Use the `useEffect` hook to fetch data when the component mounts:
4) Render data
```jsx
import React, { useState, useEffect } from 'react';

function MyComponent() {  
  const [data, setData] = useState([]);  
  const [loading, setLoading] = useState(true);  
  const [error, setError] = useState(null);

  useEffect(() => {  // Your data fetching logic goes here  
    fetch('https://api.example.com/data')  
      .then((response) => response.json())  
      .then((data) => {  
        setData(data);  
        setLoading(false);  
      })
      .catch((error) => {  
        setError(error);  
        setLoading(false);  
      });  
  }, []); // The empty array [] ensures this effect runs only once when the component mounts

  return (  
    <div> 
      {loading ? (
        <p>Loading...</p>
      ) : error ? (
        <p>Error: {error.message}</p>  
      ) : (  
        <ul>  
          {data.map((item) => (  
            <li key={item.id}>{item.name}</li>  
          ))}  
        </ul>  
      )}  
    </div>  
  );  
}
```
```