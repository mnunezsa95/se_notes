What is the DOM? (see [[JS - What is the DOM?]])

# DOM Styles
### Using Styles in the DOM (Inline)
* Styles in the DOM use camelCase
	* Styles are set using the style property
* Example
```js
const header = document.querySelector(".header__title");
header.style.backgroundColor = "orange";
```

### Using the setProperty() Method 
* The setProperty() method allows for custom properties to be changed or set on an already existing class (see [[JS - DOM Methods & Properties]])
* Example
```js
document.documentElement.style.setProperty("color-primary", "orangered");
```

# DOM Attributes
* Attributes in the DOM are actually called properties (work as objects) (see [[JS - Objects in JavaScript]])
* DOM attributes can be accessed and set using dot notation or other methods (getAttribute & setAttribute)
	* Custom attributes (non-standard) cannot be accessed this way; these are accessed using the getAttribute() method (see [[JS - DOM Methods & Properties]])
* Each HTML Element has their own attributes (not a direct one-to-one correspondence b/w HTML attributes and JavaScript properties)
	* For example: <img /> has its own attributes (alt, src, etc)
* Data Attributes are used to store extra info on standard, semantic HTML elements
* Example
```js
const logo = document.querySelector(".nav__logo"); // selecting the logo

console.log(logo.alt) // accessing the alt property
console.log(logo.alt = "Beautiful Minimalist Logo"); // setting a new value to the alt property
console.log(logo.designer); // will return undefined, because this is NOT a standard
console.log(logo.dataset.versionNumber) // accessing the versionNumber of the data attribute
```