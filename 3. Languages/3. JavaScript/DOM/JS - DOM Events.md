### What is an Event? (see [[JS - List of DOM Events]])
* An event --> something that happens on a webpage
* Events will happen whether or not we 'listen' to them
* Events have three phases (see [[JS - DOM Event Propagation]]):
	1) Capturing phase
	2) Target phase
	3) Bubbling phase

### Listening for Events
* Can be done by using:
	1) addEventListener() method (see [[JS - DOM Methods & Properties]])
		* Uses either a callback function or anonymous function (see [[JS - Callback Functions]], [[JS - Anonymous Functions]])
	2) the on event property directly on the element 
		* There is one "on event property" for every single event (see [[JS - List of DOM Events]])
	3) writing the event listener in the HTML document
* Example
```js
const h1 = document.querySelector("h1");

// using addEventListener()
h1.addEventListener("mouseenter", (evt) => {
	alert("addEventListener: Great! You are reading the heading :D")
});

// using on event property
h1.onmouseenter((evt) => {
	alert("onmouseenter: Great! You are reading the heading :D")
});
```

```html
<!-Using an event listener in HTML-->
<div class="header__title">
	<h1 onclick="alert('HTML alert')"> 
		When banking meets minimalist
	</h1>
</div>
```

### Which is preferred?
* `addEventListener()` is preferred for two reasons
	1) Can add multiple events listeners to the same event
	2) Allows you to remove event listeners using the `removeEventListener()` method
		* Can only be removed if used on a named event listener (cannot be done on arrow functions, or unnamed functions)
```js
const alertH1 = function(evt) {
	alert("addEventListener: Great! You are reading the heading :D");
	h1.removeEventListener(alertH1); // remove the event listener
}

h1.addEventListener(alertH1); // add the event listener
```

### Triggering Event Listeners during the capturing phase
* Most events have three phases: (see [[JS - DOM Event Propagation]])
	1) Capturing phase
	2) Target phase
	3) Bubbling phase
* By default event listeners are triggered during the target phase and bubbling phase (not capturing phase)
	* Events can be made to trigger during capturing phase by using the useCapture parameter (third argument) of the `addEventListener()` method (see [[JS - DOM Methods & Properties]])
```js
document.querySelector(".nav").addEventListener("click", function (e) {
	this.style.backgroundColor = randomColor();
	console.log("NAV", e.target, e.currentTarget);
}, true);
```
