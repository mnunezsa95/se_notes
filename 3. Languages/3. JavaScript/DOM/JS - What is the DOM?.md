# Intro to the Document Object Model (DOM)
* The DOM (is an interface) gives JavaScript direct access and control the HTML elements without editing HTML code

# Why is the DOM needed?
* The DOM allows for JavaScript and HTML to communicate directly with one another
	* Without the DOM, they two cannot communicate

- The DOM allows for the following: 
	1)  Manipulate existing HTML elements
	2) React to user interactions     
	3) Add new HTML elements to the page

# How do JavaScript & HTML communicate?
* Communicate is allowed due to the DOM tree
	1) The browser translates all content into a DOM tree (a format that JavaScript can understand).
		* The DOM includes the same components as an HTML document and the structure of the tree id identical to the corresponding HTML document (see [[JS - What is the DOM Tree?]]).
	2) The DOM has a variety of methods used to interact with it.

**![](https://lh3.googleusercontent.com/-qlEVUt2rUj08mnbuyontROtOQFZm3gKqEoWmT7upiOdSRd6H_StgvzehmppBGxWSsuK6r_qadgWdYsNNy-WKRE8MoZo9TeJUtQLOEZolG25eGe_E8CGrjKqVWRVRZfuLBpHFBt55swWuwKqCXZi5us)**

# Accessing the DOM
* The **document** object --> allows for the DOM of a webpage to be accessed. 