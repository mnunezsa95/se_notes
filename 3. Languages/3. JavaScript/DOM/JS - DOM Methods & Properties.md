
# DocumentNode Methods & Properties
#### document.documentElement
* Description
	* Selects the entire HTML document
* Syntax/Example
```js
console.log(document.documentElement);
```

#### document.head
* Description
	* Selects the head section of the HTML document
* Syntax/Example
```js
console.log(document.head);
```

#### document.body
* Description
	* Selects the body section of the HTML document
* Syntax / Example
```js
console.log(document.body);
```

#### document.querySelector()  
* Description
	* Returns the first Element within the document that matches the specified selector, or group of selectors (returns 'null' if not matches are found)
* Arguments
	1)  selector --> the name of the selector (can be any type of selector: class selectors, type selectors, id selectors, etc)
* Additional
	* can also be used on elements
* Syntax
```js
document.querySelector(selector);
```
* Example
```js
// Selecting an element with header class
document.querySelector('.header');
let addButton = container.querySelector('.form__submit-btn_action_add');
let resetButton = container.querySelector('.form__submit-btn_action_reset');

// can select complex selectors
let makeupBagContent = document.querySelectorAll("section.bag div.bag .item");
```

#### document.querySelectorAll()
* Description
	* Returns a static (not live) NodeList representing a list of the document's elements that match the specified group of selectors
* Arguments
	1) selector --> the name of the selector (can be any type of selector: class selectors, type selectors, id selectors, etc)
* Additional
	* can also be used on elements
* Syntax
```js
document.querySelectorAll(selectors);
```
* Example
```js
// Selecting all elements with section class
document.querySelectorAll('.section');
```

#### document.getElementById()
* Description
	* Returns an Element object representing the element whose id property matches the specified string.
* Arguments
	1) id --> The ID of the element to locate.
* Syntax
```js
document.getElementById(id);
```
* Example
```js
// Selecting all elements with section class
document.getElementById('section--1');
```

#### document.getElementsByTagName()
* Description
	* Returns a live HTMLCollection of elements with the given tag name.
* Arguments
	1) tagName --> the tag that will be located
* Syntax
```js
document.getElementsByTagName(tagName)
```
* Example
```js
// selecting all elements that have a <button> tag (returns an HTML collection)
document.getElementsByTagName('button');
```

#### document.getElementsByClassName()
* Description
	* Returns an array-like object of all child elements which have all of the given class name(s).
* Arguments
	1) names --> A string representing the class name(s) to search (multiple class names, separated by whitespace)
* Syntax
```js
document.getElementsByClassName(names)
```
* Example
```js
// Selects all elements with the classname 'btn' (returns an HTML collections)
console.log(document.getElementsByClassName('btn'));
```

#### document.createElement()
* Description
	* Creates the HTML element specified by tagName, or an HTMLUnknownElement if tagName isn't recognized.
* Arguments
	1) tagName --> A string that specifies the type of element to be created
	2) options (optional) --> An object with the following properties:
		* is --> The tag name of a custom element previously defined via customElements.define().
* Syntax
```js
document.createElement(tagName, options)
```
* Example
```js
const message = document.createElement('div');
```

---
# ElementNode Methods & Properties
#### elementNode.insertAdjacentHTML()
* Description
	* Parses the specified text as HTML or XML and inserts the resulting nodes into the DOM tree at a specified position
* Arguments
	1) [position](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML) --> A string representing the position relative to the element (options below)
		* "beforebegin"
		* "afterbegin"
		* "beforeend"
		* "afterend"
	2) text --> The string to be parsed as HTML or XML and inserted into the tree.
* Syntax
```js
elementNode.insertAdjacentHTML(position, text)
```
* Example
```js
const subject = document.querySelector("#subject");
const positionSelect = document.querySelector("#position");
subject.insertAdjacentHTML(
	positionSelect.value,
	"<strong>inserted text</strong>",
);
```

#### elementNode.innerHTML 
* Description
	* Gets or sets the HTML or XML markup contained within the element. If no HTML code, an empty string is returned.
* Syntax / Example
```js
let contents = myElement.innerHTML;
document.body.innerHTML = "";

message.innerHTML = "We use cookied for improved functionality and analytics. <button class='btn btn--close-cookie'>Got it!</button>";

document.body.innerHTML = "<h1 class='heading'>World of Web 3.0</h1>";
```

#### elementNode.textContent 
* Description
	* Allows for the text content of an element to be accessed and changed (does not impact HTML tags)
* Additional:
	* It is recommended to NOT use the **textContent** property on elements that have children since this property considers indentations and other spaces in the code to be text content. 
	* It is **recommended** to ONLY use the textContent property when dealing with elements that ONLY contain text
* Syntax / Example
```js
title.textContent = "Are NFTs the new way to collect art?"; // you can change the text content like this
```

#### elementNode.classList
* Description
	* Returns a live DOMTokenList collection of the class attributes of the element.
* Syntax / Example
```js 
const message = document.createElement('div');
message.classList; // returns a list of all classes on the 'div' element
```

#### elementNode.className
* Description
	* Gets and sets the value of the class attribute of the specified element.
* Syntax / Example
```js 
const message = document.createElement('div');
message.className;
```

#### elementNode.classList.contains()
* Description
	* Returns a boolean value — true if the class exists, otherwise false.
* Arguments
	1) token --> A string representing a token (or tokens) to be checked for existence
* Syntax
```js
elementNode.classList.add(token)
```
* Example
```js
const message = document.createElement('div');
message.classList.contains("cookie-message");
```

#### elementNode.classList.add()
* Description
	* Adds the given tokens to the list, omitting any that are already present.
* Arguments
	1) tokenN --> A string representing a token (or tokens) to add to the DOMTokenList. 
* Syntax
```js
elementNode.classList.add(token0, token1, /* …, */ tokenN)
```
* Example
```js
const message = document.createElement('div');
message.classList.add("cookie-message");
```

#### elementNode.classList.remove()
* Description
	* Removes the given tokens to the list, omitting any that are already present.
* Arguments
	1) tokenN --> A string representing a token (or tokens) to remove to the DOMTokenList.
* Syntax
```js
elementNode.classList.remove(token0, token1, /* …, */ tokenN)
```
* Example
```js
const message = document.createElement('div');
message.classList.add("cookie-message");
message.classList.remove("cookie-message");
```

#### elementNode.classList.toggle()
* Description
	* Removes an existing token from the list and returns false. Adds a nonexistent token to the list and returns true.
* Arguments
	1) token --> A string representing the token you want to toggle.
	2) force --> If included, turns the toggle into a one way-only operation. 
		* If set to false, then token will only be removed, but not added. 
		* If set to true, then token will only be added, but not removed.
* Syntax
```js
elementNode.classList.toggle(token, force)
```
* Example
```js
const message = document.createElement('div');
message.classList.toggle("cookie-message");
```

#### elementNode.classList.replace()
* Description
	* Replaces an existing token with a new token. If it does not exist, it returns 'false'
* Arguments
	1) oldToken --> the name of the token to be replaced
	2) newToken --> the name of the token that will be used to replace
* Syntax
```js
elementNode.classList.replace(oldToken, newToken)
```
* Example
```js
const message = document.createElement('div');
message.classList.add("cookie-message");
message.classList.replace("cookie-message", "cookies-for-Life");
```

#### elementNode.append()
* Description
	* Inserts a set of Node objects or string objects after the last child of the Element.
* Arguments
	1) param1, …, paramN --> a set of Node or string objects to insert.
* Syntax
```js
elementNode.append(param1, param2, /* …, */ paramN)
```
* Example
```js
message.innerHTML = "We use cookied for improved functionality and analytics. <button class='btn btn--close-cookie'>Got it!</button>";

header.append(message);
```

#### elementNode.prepend()
* Description
	* inserts a set of Node objects or string objects **before** the first child of the Element.
* Arguments
	1) param1, …, paramN --> a set of Node or string objects to insert.
* Syntax
```js
elementNode.prepend(param1, param2, /* …, */ paramN)
```
* Example
```js
message.innerHTML = "We use cookied for improved functionality and analytics. <button class='btn btn--close-cookie'>Got it!</button>";

header.prepend(message);
```

#### elementNode.before()
* Description
	* inserts a set of Node or string objects in the children list of this Element's parent, just before this Element
* Arguments
	1) param1, …, paramN --> a set of Node or string objects to insert.
* Syntax
```js
elementNode.before(param1, param2, /* …, */ paramN)
```
* Example
```js
message.innerHTML = "We use cookied for improved functionality and analytics. <button class='btn btn--close-cookie'>Got it!</button>";

header.before(message);
```

#### elementNode.after()
* Description
	* inserts a set of Node or string objects in the children list of the Element's parent, just after the Element
* Arguments
	1) param1, …, paramN --> a set of Node or string objects to insert.
* Syntax
```js
elementNode.after(node1, node2, /* …, */ nodeN)
```
* Example
```js
message.innerHTML = "We use cookied for improved functionality and analytics. <button class='btn btn--close-cookie'>Got it!</button>";

header.after(message);
```

#### elementNode.remove()
* Description
	* Removes the element from the DOM.
* Arguments
	* none
* Syntax
```js
elementNode.remove()
```
* Example
```js
document.querySelector('.btn--close-cookie').addEventListener('click', () => {
	message.remove();
})
```

### elementNode.cloneNode()
* Description
	* 
* Arguments
	* 
* Syntax
```js

```
* Example
```js

```

### elementNode.setAttribute()
* Description
	* Sets the value of an attribute on the specified element
		* If attribute already exists, the value is updated
* Arguments
	1) name --> name of the attribute whose value is to be set (in str form)
	2) value --> value to assign to attribute (in str form)
* Syntax
```js
elementNode.setAttribute(name, value)
```
* Example
```js
const logo = document.querySelector(".nav__logo"); // selecting the logo
console.log(logo.setAttribute("alt", "A beautiful minimalist logo")); // setting a new alt attribute value to the logo image

someElement.setAttribute("style", "background-color: #000000");
```

### elementNode.removeAttribute()
* Description
	* Removes the attribute with the specified name from the element.
* Arguments
	1) name --> name of the attribute to removed from the element (in str form)
* Syntax
```js
elementNode.removeAttribute(name)
```
* Example
```js
button.removeAttribute("disabled"); // removes the attribute from the element
```

### elementNode.getAttribute()
* Description
	* Returns the value of a specified attribute on the element.
* Arguments
	1) attributeName --> name of the attribute whose value you want to get.
* Syntax
```js
elementNode.getAttribute(attributeName)
```
* Example
```js
const logo = document.querySelector(".nav__logo"); // selecting the logo
console.log(logo.getAttribute(designer)); // gets the designer attribute of the logo element (designer is not a standard attribute, so needs to be accessed this way)
```

### elementNode.scrollIntoView()
* Description
	* Scrolls the element's ancestor containers to make it visible to the user
* Arguments
	1) scrollIntoViewOptions --> An Object with the following properties
		* behavior --> determines whether scrolling is instant or animates it smoothly (in str form); the options are:
			* "Smooth"
			* "instant"
			* "auto"
		* block --> defines vertical alignment 
			* "start"
			* "center"
			* "end"
		* inline --> defines horizontal alignment
			* "start"
			* "center"
			* "nearest"
* Syntax
```js
elementNode.scrollIntoView(scrollIntoViewOptions)
```
* Example
```js
btnScrollTo.addEventListener("click", function (e) {
  const s1coords = section1.getBoundingClientRect();
  section1.scrollIntoView({ behavior: "smooth" });
});
```

### elementNode.getBoundingClientReact()
* Description
	* Returns a DOMRect object providing information about the size of an element and its position relative to the viewport.
* Arguments
	* None
* Syntax
```js
elementNode.getBoundingClientReact();
```
* Example
```js
const navHeight = nav.getBoundingClientRect(); // will return the DOMReact object providing info about the size of an element and its position relative to the viewport
navHeight.height // provides info about the height relative to the viewport
```

#### elementNode.style
* Description
	* Allows to style an element using CSS declarations (see [[JS - DOM Styles, Attributes and Classes]]) like an inline style
	* Functions like <style></style> attribute in HTML
* Additional
	* List of all [Element Node Attributes](https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/style)
* Syntax / Example
```js
elementNode.style.backgroundColor = '#37383d'
elementNode.style.height = "30px"
```

--- 
# CSS Style Declaration Methods

#### setProperty() 
* Description
	* Sets a new value for a property on a CSS style declaration object
* Arguments
	1) propertyName --> the CSS property name (hyphen case) to be modified (in str form)
	2) value --> the new property value (in str form)
	3) priority (optional) --> A string allowing the "important" CSS priority to be set. Accepts the following: `important`, `undefined`, `" "` 
* Syntax
```js
setProperty(propertyName, value, priority)
```
* Example
```js
document.documentElement.style.setProperty("color-primary", "orangered");
```

#### window.getComputedStyle()
* Description
	* Returns an object containing the values of all CSS properties of an element
* Arguments
	1) element --> the element for which to get computed style
	2) pseudoElt --> A string specifying the pseudo-element to match. 
* Syntax
```js
getComputedStyle(element, pseudoElt)
```
* Example
```js
getComputedStyle(message).color // gets the computed color style
getComputedStyle(message).height // gets the computed height
message.style.height = Number.parseFloat(getComputedStyle(message).height + 10) + 30 + 'px';
```

---
# DOM Event Methods

#### elementNode.addEventListener()
* Description 
	* Sets up a function that will be called whenever the specified event is delivered to the target.
* Arguments
	1) eventType --> a string identifying the event type to listen for
	2) listenerFn --> a callback function that will be executed when the event happens 
		* (usually uses the following format: `handleSomething`)
	3) options (optional) --> specifies characteristics about the event listener; possible options are: 
		* capture --> A boolean value indicating that events of this type will be dispatched to the registered listener before being dispatched to any EventTarget beneath it in the DOM tree
		* once --> A boolean value indicating that the listener should be invoked at most once after being added (if `true` listener is removed after being invoked)
		* passive --> A boolean value that, if true, indicates that the function specified by listener will never call preventDefault().
		* signal --> The listener will be removed when the given `AbortSignal` object's [`abort()`](https://developer.mozilla.org/en-US/docs/Web/API/AbortController/abort "abort()") method is called
	4) useCapture (optional) --> a boolean to state whether the event should be triggered during capture phase. If set to true, events will be listened to during capturing phase
* Syntax
```js
elementNode.addEventListener(eventType, listenerFn, options, useCapture)
```

* Example
```js
const h1 = document.querySelector("h1");

// using addEventListener()
h1.addEventListener("mouseenter", (evt) => {
	alert("addEventListener: Great! You are reading the heading :D")
});


// using addEventListener with a named function
function showClick() {
  console.log("You have clicked on the element");
}
element.addEventListener("click", showClick);
```
#### elementNode.removeEventListener()
* Description
	* Removes an event listener previously registered with EventTarget.addEventListener() from the target
* Arguments
	1) type --> a string that specifies the type of event to remove from the eventTarget
	2) listener --> The event listener function of the event handler to remove from the event target.
	3) options (optional) --> An options object that specifies characteristics about the event listener. Possible options are:
		* capture --> A boolean value that specifies whether the [event listener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener#the_event_listener_callback) to be removed is registered as a capturing listener or not.
* Syntax
```js
elementNode.removeEventListener(type, listener, options)
elementNode.removeEventListener(type, listener, useCapture)
```
* Example
```js
const alertH1 = function(evt) {
	alert("addEventListener: Great! You are reading the heading :D");
	h1.removeEventListener(alertH1); // remove the event listener
}

h1.addEventListener(alertH1); // add the event listener
```

#### event.preventDefault()
* Description
	* Prevents the default browser behavior 
* Arguments
	* None
* Syntax
```js
event.preventDefault();
```
* Example
```js
const form = document.querySelector(".form");

form.addEventListener("submit", function (evt) {
  // disable the default action that belongs to the event
  evt.preventDefault();
  // check the user data
}); 
```

#### event.stopPropagation()
* Description
	* Prevents further propagation of the current event in the capturing and bubbling phases
* Arguments
	* None
* Syntax
```js
event.stopPropagation()
```
* Example
```js
document.querySelector(".nav__link").addEventListener("click", function (e) {
this.style.backgroundColor = randomColor();
e.stopPropagation(); // propagation will NOT occur
});
```

---

# DOM Traversing Properties


#### node.childNode
* Description
	* Returns a live NodeList of child nodes of the given element where the first child node is assigned index 0.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));
console.log(h1.childNodes); // returns NodeList of all child nodes of the h1 element.
```

#### elementNode.children
* Description
	* Returns a live HTMLCollection which contains all of the child elements of the specified element
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));
console.log(h1.children); // returns HTMLCollection of all IMMEDIATE children of the h1 element.
```

#### elementNode.firstElementChild
* Description
	* Returns the node's first child in the tree, or null if the node has no children.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

h1.firstElementChild.style.color = 'white'; // sets the style of the first child element of the h1 element to white
```

#### elementNode.lastElementChild
* Description
	* Returns an element's last child Element, or null if there are no child elements.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

h1.lastElementChild.style.color = 'orangered'; // sets the style of the last child element of the h1 element to orangered
```

#### node.parentNode
* Description
	* Returns the parent of the specified node in the DOM tree.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.parentNode) // returns the parent node of the h1 element (could be document node, text node, or comment node), it will simply return the one above it
```

#### elementNode.parentElement
* Description
	* Returns the DOM node's parent Element, or null if the node either has no parent, or its parent isn't a DOM Element.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.parentElement); // returns the parent element of the h1 element
```


#### node.previousSibling
* Description
	* Returns the node immediately preceding the specified one in its parent's childNodes list, or null if the specified node is the first in that list.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.previousSibling); // returns the immediate sibling node before the h1 element
```

#### elementNode.nextSibling
* Description
	* Returns the node immediately following the specified one in their parent's childNodes, or returns null if the specified node is the last child in the parent element.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.nextSibling); // returns the immediate sibling node before the h1 element
```

#### elementNode.previousElementSibling
* Description
	* Returns the Element immediately prior to the specified one in its parent's children list, or null if the specified element is the first one in the list.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.previousElementSibling); // returns the immediate sibling element before the h1 element
```

#### elementNode.nextElementSibling
* Description
	* Returns the element immediately following the specified one in its parent's children list, or null if the specified element is the last one in the list.
* Syntax/Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

console.log(h1.nextElementSibling); // returns the immediately sibling element after the h1 element
```


# DOM Traversing Methods

### elementNode.closest() 
* Description
	* Traverses the element and its parents (heading toward the document root) until it finds a node that matches the specified CSS selector.
		* Can be considered to be the opposite of `querySelector()`
* Arguments
	1) selectors --> a valid CSS selector (in str form) to match the element and its ancestors against
* Syntax
```js
elementNode.closest(selectors)
```
* Example
```js
const h1 = document.querySelector('h1');
console.log(h1.querySelectorAll('.highlight'));

h1.closest('.header').style.backgroundColor = "var(--gradient-secondary)";
// will search for the element closest to h1 with a 'header' class and apply color to that element
```

### 
* Description
	* 
* Arguments
	1) 
* Syntax
```js

```
* Example
```js

```

### 
* Description
* Arguments
	1) 
* Syntax
```js

```
* Example
```js

```

### 
* Description
* Arguments
* Syntax
```js

```
* Example
```js

```

### 
* Description
* Arguments
* Syntax
```js

```
* Example
```js

```

### 
* Description
* Arguments
* Syntax
```js

```
* Example
```js

```