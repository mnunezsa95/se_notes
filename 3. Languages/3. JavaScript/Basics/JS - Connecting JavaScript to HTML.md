See [[JS - What is the DOM?]], [[JS - What is the DOM Tree?]]

Resources
* [TripleTen: JavaScript Basics Cheatsheet](https://practicum-content.s3.us-west-1.amazonaws.com/web-developer/cheat-sheet/js-basics.pdf)

# Adding JavaScript to a Webpage
* The `<script>` tag is used to connect JavaScript to the HTML document
	* The `<script>` can be used in two ways:
		1) Write JavaScript code between the <script></script> tags directly in the HTML document
		2) Write JavaScript code in a separate file and connect it with the HTML document using the `src` attribute of the <script></script> by placing it below the closing `</body>` tag
* Example
```html
<script src="script.js"></script>
```

### Adding Loading Attributes
* There are 3 ways to load JavaScript files in HTML
	1) Regular loading
	2) Async loading
	3) Defer loading
* The location in which the three options are used also has an effect on load time.

### Summary: Which Strategy is the best
* Using "defer" in the <head></head>

### Loading Comparison

**![](https://lh4.googleusercontent.com/ujDr0_tHaR0y145KK0K3ljqT5WSOLK5ZBhM1gQuh8sWOJ8zRFCLh5e4COgfxTKMTe7VIUAY30mCpFJUo0hS0UGrJ2syI33pWCs1TInij_YXa_HD7Cywn-0AAH8ZBCh8sGAi_UXUUvtTpOXwTZvR_dAE)**

**![](https://lh6.googleusercontent.com/voWF485Ttqf5BgwdPSQgPibtN1-10rBzh9pwpWXNWLXeyCy181OvSAEq79qHijBzoGhnuueArrv_p79voLoXmID0TuKHBqCLDB3NWGZnoYm2d07ptl9K_Nnoyd7C-8fSZI8LrRbTP0bZT6ncJJWy2hA)