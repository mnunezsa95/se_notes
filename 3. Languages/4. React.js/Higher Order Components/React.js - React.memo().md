See [[React - Introduction to React.js]], [[React.js - Higher Order Components]]
Resources:
* [10 Expert Performance Tips Every Senior JS React Developer Should Know](https://medium.com/@khushi1399gupta/10-expert-performance-tips-every-senior-js-react-developer-should-know-a786fc13f5c7)

---

#### What is `React.memo()`?
* `React.memo()` is a higher-order component for functional components
* It optimizes the rendering process by ONLY allowing re-renders when the component's props have shallowly changed

#### Example: Comparing a regular component with one `React.memo()`
* A regular component
```JSX
// Regular functional component  
const TitleRegular = ({ text }) => {  
  console.log("Rendering Regular Title...");  
  return <h2>{text}</h2>;  
};
```
* A component wrapped in `React.memo()`
	* By wrapping the component with React.memo, it prevent excessive re-renders and boost performance.
```JSx
// Memoized functional component using React.memo  
const TitleMemoized = React.memo(({ text }) => {  
  console.log("Rendering Memoized Title...");  
  return <h2>{text}</h2>;  
});
```
