### Resources
* [Intersection Observer API: MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)

### What is the Intersection Observer API?
* Allows code to
	* Observe changes to the way that a certain target element intersects another element or the viewport
* Provides a way to
	* asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document's viewport.*
### Using the Intersection Observer API
1) Create a new instance of the `IntersectionObserver()`
	* Two arguments
		1) callback --> gets called each time that the observed element is intersecting the root element at the specified threshold; takes two arguments
			1) entries --> list of entries received by the callback includes one entry for each target which reported a change in its intersection status
			2) observer --> 
		2) options --> controls the circumstances under which the observer's callback is invoked
			* root --> the root element that the target will be intersecting
			* rootMargin --> the margin around the root (in pixels)
			* threshold -->  the percentage of intersection at which the observer callback will be triggered

2) Call the `observe()` method on the new instance of the `IntersectionObserver()`
	* This will 

```js
const navHeight = nav.getBoundingClientRect().height;
const stickyNav = function (entries) {
const [entry] = entries;
	if (!entry.isIntersecting) {
		nav.classList.add("sticky");
	} else {
		nav.classList.remove("sticky");
	}
};

const obsOptions = {
	root: null,
	threshold: [0],
	rootMargin: `-${navHeight}px`,
};

const headerObserver = new IntersectionObserver(stickyNav, obsOptions);
headerObserver.observe(header);
```

# Intersection Observer API Properties
1) boundingClientRect -->
2) intersectionRatio -->
3) intersectionRect --> 
4) isIntersecting -->
5) isVisible -->
6) rootBounds --> 
7) target -->
8) time -->