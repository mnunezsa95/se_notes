## What is the try...catch statement
* A syntax used for catching errors in a block of code
	* Commonly used to wrap `async/await` functions since they cannot use the traditional `then...catch` statements (see [[JS - Async & Await]])

### The “try…catch” syntax
* Three main blocks: 
	1) try --> the code block that will be executed
	2) catch --> the code that is executed if an error is detected
	3) finally --> describe a code block to run regardless of the result (before control flow exists)
```js
try {
  // code to be executed
} catch (err) {
  // error handling code to be executed if error is detected
}
```


**![](https://lh3.googleusercontent.com/vf1yYeVw1Zg2e5F8GDD3xOtAVpD7y3KzqzhBlf4Y1XnaNwmwKGFr0EwNvTFyIkKEllIw2iv0sBj8maKXkL3UkoHeqR4tLLtZHTkvCvZ5nvZAtvxSYK4vsbvsT6dp7-iTeM4d2OtOuK9oxYuG_N_KQFY)**

#### Examples
```js
// Simple try...catch statement

try {
	let y = 1;
	const x = 2;
	x = 3; // will produce an error (x is defined with const)
} catch (err) { // catches any errors detected
	console.log(err); 
}
```

```js
try {
	adddlert("Welcome guest!"); // will not execute b/c error
} catch (err) {
	document.getElementById("demo").innerHTML = err.message;
}
```

```js
const whereAmI = async function () {
	try { 
		// Geolocation
		const pos = await getPosition();
		const { latitude: lat, longitude: lng } = pos.coords;
		
		// Reverse geocoding
		const resGeo = await fetch(
			`https://geocode.xyz/${lat},${lng}?geoit=json`
		);
		if (!resGeo.ok) throw new Error('Problem getting location data');
		const dataGeo = await resGeo.json();
		
		// Country data
		const res = await fetch(
			`https://restcountries.eu/rest/v2/name/${dataGeo.country}`
		);
		
		if (!res.ok) throw new Error('Problem getting country');
		const data = await res.json();
		renderCountry(data[0]);
		
	} catch (err) {
		console.error(`${err} 💥`);
		renderError(`💥 ${err.message}`);
	}
};
```