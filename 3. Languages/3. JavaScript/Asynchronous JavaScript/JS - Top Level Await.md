### What is a top level await?
* Allows await to be used outside of an **async function** (see [[JS - Async & Await]])
	* Can ONLY be used in a **MODULE** (see [[JS - What are Modules?]])
* Blocks the execution of the entire MODULE 
	* Can be harmful if the execution takes a long time

* Example: Simple
```js
// await can be used at the top level (outside of an async function)
const res = await fetch('https://jsonplaceholder.typicode.com/posts');
const data = await res.json();
console.log(data);
```

* Example: Complex
```js
// Function to fetch the last post
const getLastPost = async () => {
	const res = await fetch('https://jsonplaceholder.typicode.com/posts');
	const data = await res.json();
	console.log(data);
	
	return { title: data.at(-1).title, text: data.at(-1).body };
};

// Using top-level await removes the need for handling the return promise using then()
const lastPost = await getLastPost();
console.log(lastPost);
```