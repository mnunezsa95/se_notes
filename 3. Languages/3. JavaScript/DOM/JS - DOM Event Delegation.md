Resources
* [Event Delegation in JavaScript –Explained with an Example](https://www.freecodecamp.org/news/event-delegation-javascript/#:~:text=Event%20Delegation%20is%20a%20pattern,the%20event%20was%20first%20received.)

# What is Event Delegation
* An event handling pattern based upon the concept of Event Bubbling (see [[JS - DOM Event Propagation]]) 
* Allows us to handle events at a higher level in the DOM tree (other than the level where the event was first received)

# How does Event Delegation Work
* Works on the following principal
	* Handling events in a common parent (instead of the actual element that received the event)
* The event object has a `target` property which contains information about the element that actually received the event (see [[JS - DOM Event Object & Target Events]])

# Benefits of Event Delegation
* Provides cleaner code
* Needs fewer event listeners (with similar logic)

# Performing Event Delegation
* Event delegation uses two basic steps
	1) Add the event listener to a common parent element
	2) Determine what element originated the event (to work with that element)
		* The `evt.target` property and `classList.contains()` method can be used for this (see [[JS - DOM Methods & Properties]])
* Example
```js
// Adding event listener to the common parent (nav__links)
document.querySelector(".nav__links").addEventListener("click", function (evt) {

	// Matching strategy (ensuring it will ONLY work when an actual nav__link           element is clicked)
	if (evt.target.classList.contains("nav__link")) {
		evt.preventDefault();
		const id = evt.target.getAttribute("href");
		document.querySelector(id).scrollIntoView({ behavior: "smooth" });
	}
});
```