### What is the Event Object?
* Accessible as parameter of the `addEventListener()` method (see [[JS - DOM Methods & Properties]])
* Contains information about the event that occurred and the element the triggered the event
	* Can be used in the body of the function
* Typically named either: `event`, `e` or `evt
* Example
```js
const likeButton = document.querySelector(".song__like-btn");

// event is available as a parameter
likeButton.addEventListener("click", function (evt) { 
    console.log(evt); // you can use it in the body of the handler
}); 

```

### Preventing default behavior
* The `preventDefault()` method of the event object prevents any unwanted actions that are automatically performed by the browser (see [[JS - DOM Methods & Properties]])

### The Target Property
* DOM events are directly linked to Event Propagation (see [[JS - DOM Event Propagation]])
* There are two types of Target properties:
	* `evt.target `--> what triggers the event
	* `evt.currentTarget` --> what the event listener is assigned to
		* In any event handler, the `'this'` keyword is the same as the `e.currentTarget`

* Examples
```js
const button = document.querySelector(".button");

button.addEventListener("click", function (evt) {
	// the evt.target will contain the button element that we clicked on
	const eventTarget = evt.target;
    eventTarget.setAttribute("disabled", true);
}); 
```


```js
document.querySelector(".nav__link").addEventListener("click", function (e) {
	this.style.backgroundColor = randomColor();
	console.log("LINK", e.target, e.currentTarget);
});

document.querySelector(".nav__links").addEventListener("click", function (e) {
	this.style.backgroundColor = randomColor();
	console.log("CONTAINER", e.target, e.currentTarget);
});

document.querySelector(".nav").addEventListener("click", function (e) {
	this.style.backgroundColor = randomColor();
	console.log("NAV", e.target, e.currentTarget);
	console.log(e.currentTarget === this); // will return true because these two are equal to each other
});
```