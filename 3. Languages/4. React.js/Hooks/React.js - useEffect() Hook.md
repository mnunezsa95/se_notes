See [[React - Introduction to React.js]]
Resources:
* [React: You are Using useEffect() Wrong, Do This Instead](https://blog.stackademic.com/why-you-should-avoid-using-useeffect-hook-in-react-and-what-to-do-instead-740660e33420)
* 

---
#### `useEffect()` 
* A react hook used to handle side-effects
* Receives two inputs
	* A callback function
	* A list of dependencies -> defines when the hook is called
```JSX
useEffect((prevProps) => {  
  // custom function content…  
  return () => {  
  // Code to run when the component is unmounted or when dependencies change  
  // It helps in avoiding memory leaks and unexpected behavior  
  };  
}, [dependencies in array form]);
```
* Dependencies
	* Case A: If nothing is added, then `useEffect()` will run at every change of state inside the current component.
	* Case B: If an empty array is added ([]), then the `useEffect()` will run only once when the component is mounted.
	* Case C: If some array is provided (`[state]`), then `useEffect()` will run every time the state changes
	* Case C*: If some array is provided (`[state1, state2, ….]`, `useEffect()` will run every time **ANY** of these states changes.