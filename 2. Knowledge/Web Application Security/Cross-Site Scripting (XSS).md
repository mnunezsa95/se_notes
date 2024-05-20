# What do XSS Attacks do?
* XSS attacks inject malware into the page that the server sends to the user

#### Causes of XSS
* Old browser versions
* Unregulated user input
* Lack of Content Security Policy standard implementation
* Numerous third-party dependencies (could contain malicious code)

---
# Protecting against XSS
#### Browser Protection
* Chromium based engines protect against some attacks
* Other engines (like internet explorer) are not protected

#### Restrict User Input
* Applying the "anything not allowed is explicitly forbidden" principal
* Example: making it so each input field can ONLY contain specific characters 

#### Escape Characters
* Special characters (such as: `<` & `>`) can be escaped so they are not perceived as code
	* Protects users against script injection attacks
* How to escape characters
	* Replace the special character with the HTML entity 
* Node.js has a module called `escape-html` that automatically substitutes these escape entities into the code (see [[Node.js - Module - escape-html]])
* Example
```js
// replacing this line with the HTML entity for < 
'Inequality x * 2 < 4 is correct if x < 2'; 

'Inequality x * 2 &lt; 4 is correct if x &lt; 2'; 
```

```js
// the hacker's script:
Kevin+<script>alert('Hacked!');</script>

// what the user actually gets: hacker script doesn't work
Kevin+&lt;script&gt;alert('Hacked!');&lt;/script&gt; 
```
#### Content Security Policy
* The Content Security Policy standard --> allows for the the site to restrict the sources form which scripts, images, stylesheets and media files are loaded
* Two ways of using the content-security policy
	1) Using the `<meta>` tag in the `<head>`
	2) Use an HTTP header, with instructions (each statement ends in semi-colon)  (see [[Node.js - The Request Object]])
		* Instructions possibilities
			* `default-src` — a mandatory instruction that sets the source of all kinds of resources by default
			* `script-src` — permitted source of scripts
			* `img-src` — permitted source for images
			* `media-src` — permitted source for audio and video files
			* `style-src` — permitted source for style files
		* Using the `self` keyword
			* specifies the domain of the site as the src

```html
<!--Using the <meta> tag-->
<meta http-equiv="Content-Security-Policy" content="INSTRUCTIONS">
```

```
// Using the request header

Content-Security-Policy: 
	default-src 'self'; 
	img-src *; 
	media-src media1.com media2.com; 
	script-src userscripts.example.com 
```

#### Checking the browser version
* Newer browsers are usually more secure 
	* Restricting older browsers (can be a good move) --> not user friendly approach

* How to check browser version
	* Browsers send information about their version in any request inside the `User-Agent` header using the general format below
```
User-Agent: <product> / <product-version> <comment> 
```

```
user-agent: 
	Mozilla/5.0 (Windows NT 10.0; Win64; x64) 
	AppleWebKit/537.36 (KHTML, like Gecko) 
	Chrome/77.0.3865.90 
	Safari/537.36 
```