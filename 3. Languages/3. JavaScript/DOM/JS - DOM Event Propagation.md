### What are events?
* More information (see [[JS - DOM Events]])

# Event Propagation
* Most events have a capture, target and bubble phase
	* Some execute directly in the target phase
**![](https://lh6.googleusercontent.com/O2Zv25cyzDcUQ6CoZhPSVFEi1IY9GNhaUQhRlu6vpnTXsWHsoS4pf5WdV25NB2Cy3xqUVaVkjT2TVLCb3_sTQDWCS4ICJKSCEgXol9DWM1CpIS2-fzqZ33xMwn0Uvqy8F4SothNWEYvYboJfR5_GaRg)
* When an event happens, it does not happen at the target element
	* Events happen at the root document (top of DOM tree) (see [[JS - What is the DOM Tree?]])
* The event triggers the capturing phase
	* Capturing phase --> event travels down to the element where the event happens 
		* Event passes every parente element
* When the event reaches the target, the target phase begins
	* Target phase --> events are handled (two parts)
		* Event is listened for by the event listener/handler
		* Event happens
* Once event happens, the bubbling phase starts
	* bubbling phase --> events travel back up to the top of the DOM tree
		* Event passes through all parent elements
		* Events actually happen at parent elements on the way back up to the DOM (bubbling phase)
			* If then same event listener is used on parent, it will also execute

### Example
```js
// create a random Integer
const randoInt = (min, max) => Math.floor(Math.random() * (max - min + 1) + min);

const randomColor = () => `rgb(${randoInt(0, 255)},${randoInt(0, 255)}),${randoInt(0, 255)})`; // create a random color

// will turn the "Features" nav link a random color
document.querySelector(".nav__link").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
});

// will also be executed when the "features" link it clicked because of bubbling (this is the parent element to .nav__link)
document.querySelector(".nav__links").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
});

// will also be executed when the "features" link it clicked because of bubbling (this is the parent element to .nav__links, and grandparent to nav__link)
document.querySelector(".nav").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
});
```

**![](https://lh4.googleusercontent.com/PMV7bC3c4xH0vqgXLZqfRODRQa8p_eCGapfHVxHT79QWq_atGtYJS6R63TtsYVmkmD7Q7gkFIck7HycrUNI-8_sqgJ7Djb2V8chWovPI5Qqaj4h3Pty49y4dmq6gfKXZh6IZ72kWxJcM8X65UGhnizc)**

# Stopping Propagation
* Propagation can be stopped using the `e.stopPropagation()` method (see [[JS - DOM Methods & Properties]])
* Stopping propagations --> generally not a good idea, but can be helpful

```js
// create a random Integer
const randoInt = (min, max) => Math.floor(Math.random() * (max - min + 1) + min);

const randomColor = () => `rgb(${randoInt(0, 255)},${randoInt(0, 255)}),${randoInt(0, 255)})`; // create a random color

// will turn the "Features" nav link a random color
document.querySelector(".nav__link").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
	e.stopProgation(); // will prevent this event from bubbling back up to the parent elements
});

// will not be executed because of the stopProgation() method
document.querySelector(".nav__links").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
});

// will not be executed because of the stopProgation() method
document.querySelector(".nav").addEventListener("click", function (evt) {
	this.style.backgroundColor = randomColor();
});
```