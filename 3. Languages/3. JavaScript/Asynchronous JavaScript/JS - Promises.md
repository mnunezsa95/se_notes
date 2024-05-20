### What is a Promise?
* An object (as a placeholder) for future value of an asynchronous operation
	* Simple: "A container for a future value"
* Used to handle the future value

### Benefits of Promises
* Removes need for using events & callbacks to handle asynchronous results
* Allows for chaining promises for a sequence of asynchronous operations (no more callback hell)

### Lifecycle of a Promise
* Pending = before a result
* Settled = when the asynchronous task is done
	* Fulfilled --> successfully provided a result
	* Rejected --> when an error happens
* Consumed --> when a promise if created
* Build Promise --> creates a promise (see [[JS - Building a Promise]])

**![](https://lh6.googleusercontent.com/oeK8VOpTSx-lB8_zdMitTu91dvbiiqbZjoC7PLDDYWVZzgnf08QXDFWbe-AD_zCWyO35pUDO8A_HdL6fE6AojncWl4w6GfIlxEQ45PD5P8-Jw6cvm3yNEe15NHDVpvXwL-gXSa5hOGt_cTr8gIBtbhM)**

### Working with Promises 
* Methods for working with promises (see [[JS - Promise Methods]])
	* then()
	* catch()
	* finally()

### Chaining Promises
[Udemy Video: Chaining Promises](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/22649327?start=0#overview)
* Multiple **Promises** can be chained together 
	* The **then()** method always returns a promise (even if something is returned or not)
		* If value is returned, the returned value becomes the fulfilled value of the promise
```js
const getCountryData = function (country) {
  fetch(`https://restcountries.com/v3.1/name/${country}`)
    .then(res => res.json()) // convert the response to json
    .then(data => { // do something with the data
      renderCountry(data[0]);
      const neighbor = data[0].borders[0];
      if (!neighbor) return;
      return fetch(`https://restcountries.com/v3.1/alpha/${neighbor}`); 
      // return a promise 
    })
    .then(res => res.json()) // convert the response from last promise
    .then(newData => { // do something with the data
      renderCountry(newData);
    });
};
```