What is the Geolocation API? (see [[Geolocation API]])
# Geolocation Retrieval Methods

### Geolocation.getCurrentPosition()
* [Description](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/getCurrentPosition)
	* Gets the current position of the device
* Arguments
	1) success --> a callbackFn that takes the `GeolocationPosition` object as an input
	2) error (optional) --> a callbackFn that takes a `GeolocationPositionError` object as an input	
	3) options (optional) --> An optional object including the following parameters
		* maximumAge
		* timeout
		* enableHighAccuracy
* Syntax
```js
geolocation.getCurrentPosition(success, error, options);
```
* Example
```js
const sucessfulCallback = (position) => {
  const { latitude } = position.coords;
  const { longitude } = position.coords;
  console.log(`https://www.google.com/maps/@${latitude},${longitude}`);
};

const handleError = () => {
  console.log("error");
};

if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(sucessfulCallback, handleError);
}
```

### Geolocation.watchPosition()
* Description
* Arguments
	1) 
* Syntax
```js

```
* Example
```js

```