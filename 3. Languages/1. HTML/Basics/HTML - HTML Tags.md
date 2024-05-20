See [[HTML - Introduction to HTML]]

---
## Tags
* All HTML elements are composed of an opening tag and a closing tag (some elements have self closing tags)
	* Different tags allow for different `attributes`, which provide more information as to how the element should behave. 
		* Attributes are placed inside the opening tag using the `name=value` format.
```HTML
<!--id is an attribute of the table tag and its value is "student"-->
<table id="student" class="Stanford"> 
```


#### `<html> </html>`
* The `<html>` tag introduces each HTML document and indicates its beginning, while `</html>` marks its end
	* The `<head>` and `<body>` of the HTML document are found between these tags.

#### `<head> </head>`
* These tags mark the document's heading. Tags introducing the document's title (`<title>`) and meta (additional) information (`<meta>`) are placed between these tags.

#### `<body>` `</body>`
* The `<body>` tag marks the beginning of the body of an HTML page. All the contents of the page (headings, text paragraphs, tables, images) are placed within the body.

#### `<p>` `</p>`
* The `<p>` HTML element represents a paragraph. Text is often placed within this _p_ (paragraph) element.

#### `<div> </div>`
* The `<div>` (division) block tag wraps various elements. 
	* `<div>` is useful since it can incorporate any number of elements, even of different kinds (e.g. a header with an image plus a couple of text paragraphs), and assign them common features or behavior. 

#### `<table> </table>`
* The `<table>` HTML element represents tabular data—that is, information presented in a two-dimensional table comprised of rows and columns of cells containing data.
	* The contents of the table are divided into rows by `<tr>` (table row) tags, and rows, in turn, are divided into cells by `<td>` (table data) tags.
	* The `<th>` (table header) tags represent the table headers and are often placed in the first row (`<tr>`) tags