See [[JS - Introduction to JavaScript]]

---

#### What is a Memory Leak?
* A memory leak in JavaScript occurs when a program reserves memory for objects or data that are no longer needed or referenced, preventing the JavaScript engine’s garbage collector from freeing up that memory.

#### Why are Memory Leaks Harmful?
* **Performance**: Memory leaks can accumulate over time, making applications sluggish and even leading to crashes.
* **Resource Consumption**: Memory leaks increase the amount of system resources your application consumes, affecting other processes running on the user’s device.

#### Tools for Tracking Leaks
* **Chrome DevTools Memory Profiler** -> Tracks memory usage, spots leaks and helps understand overall memory footprint of web applications

#### Top causes of Memory Leaks
1) Uncleared Intervals and Timers
	* **Issue**: Not clearing`setInterval` and `setTimeout` when no longer needed
	* **Mitigation**: Use `clearInterval` and `clearTimeout` to remove timers and intervals when no longer needed
```JavaScript
const someData = fetchLatestData(); // A hypo function that fetches some data  
  
const intervalID = setInterval(() => {  
  updateUI(someData);  
}, 1000);  
  
// Later in the code or in some cleanup routine, the interval needs to be cleared. If not: clearInterval(intervalID);
```

2) Dangling Event Listeners
	* **Issue***: Forgetting to remove event listeners after they have served their purpose
	* **Mitigation**: Use the `removeEventListener` method to detach listeners when they're no longer required or when associated elements are removed from the DOM.
```JS
const buttonElement = document.querySelector("#submit-button");  
const userPreferences = getUserPreferences(); // Hypo function  
  
buttonElement.addEventListener('click', () => {  
  applyPreferences(userPreferences);  
});  
  
// Now, if for any reason, the button is removed from the DOM: buttonElement.remove();  
// The listener is still in memory and so is the 'userPreferences' object.
```

3) Closures
	* **Issue**: Closures can unintentionally hold onto references, leading to memory leaks.
	* **Mitigation**: Be mindful of what closures reference, especially if those references include large objects or DOM
```JS
function createLogger(element) {  
const loggingInfo = getLoggingInfo(); // Hypo function fetching some  data  
  return function log() {  
    console.log(element, loggingInfo);  
  };  
}  
  
const someElement = document.querySelector("#info-box");  
const logger = createLogger(someElement);  
someElement.addEventListener('mouseover', logger);  
  
// If 'someElement' is removed from the DOM or no longer used, the closure 'logger' still retains references.
```

4) Retained DOM Elements
* **Issue**: After removing a DOM element from a page, any references to it (such as storing it in a variable) can prevent it from being garbage collected
* **Mitigation**: Nullify or remove references to DOM elements once they are no longer needed.
```JS
const element = document.createElement('div');  // Storing a reference to the el
const container = document.getElementById('container');  
container.appendChild(element);  
container.removeChild(element);  // removing the element from the container  

// Failing to remove the reference to the el
```