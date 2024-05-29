See: [[Node - Introduction to Node.js]]
#### Resources
* [Understanding Streams in Node.js](https://nodesource.com/blog/understanding-streams-in-nodejs/)
	* In Node.js, creating a server doesn't require using streams, and, when using Express, we have access to a body parsing middleware.
	* When working with large data take advantage of streams in order to build a more robust application

--- 
What is a stream? (see [[Node.js - Processing Request Data]])

### Types of Streams
There are 4 types of streams:
1) **Readable**: streams from which data can be read
2) **Writable**: streams from which data can be written
4) **Duplex**: streams from which data can be read and written
5) **Transform**: a type of duplex stream from which data can be modified while being read and written
### What are Streams?
* Streams carry information (see [[Node.js - Module - fs]])

### readFile() & writeFile() vs createReadStream() & createWriteStream()
* Using readFile() & writeFile() requires more memory to process each file
* Using createReadStream() & createWriteStream() allows data to be read in small chunks
	* Stores on 'chunk' at a time
	* More efficient in terms of memory consumption

### Creating Readable and Writable Streams
* The fs module (see [[Node.js - Module - fs]]) has methods for creating readable and writable streams with streams (see [[Node.js - Methods]])
* Example
```js
const fs = require('fs'); 

// create a readable stream from the in.txt file 
const reader = fs.createReadStream('./in.txt', { encoding: 'utf8' }); 

// create a writable stream to the out.txt file 
const writer = fs.createWriteStream('./out.txt', { encoding: 'utf8' });
```

### Creating a Duplex Stream
* Duplex streams, require the stream to be readable first
* Duplex streams can be simplified using the pipe() method (see [[Node.js - Methods]])
* How to create a Duplex Stream?
	1) Use of the **'data'** event on readable streams via the on() listener (see more on 'data' event [[Node.js - The Request Object]])
		* 'data' request triggered when data is received
	2) Use the **'end'** event on a listener to trigger when there is no more data to be consumed from the stream
		* 'end' event ends the stream
	3) Use the end() method on the writable stream
	4) Use the 'error' event on a listener to trigger if there is an error
		* 'error' event handles error
```js
const fs = require('fs');

// create read and write stream
const reader = fs.createReadStream('./in.txt', { encoding: 'utf8' }); 
const writer = fs.createWriteStream('./out.txt', { encoding: 'utf8' });

reader.on('data', (chunk) => { // attach on() listener to readable stream
	writer.write(chunk); // write chunk of data to the writable stream
});

reader.on('end', () => { // 'end' event signals to node (no more data coming in)
	writer.end(); // the end() method of the writable stream ends 'writing'
});

reader.on('error', (err) => { // 'error' event triggers if there is an error
	console.log(err)  // logs the error
})
```

