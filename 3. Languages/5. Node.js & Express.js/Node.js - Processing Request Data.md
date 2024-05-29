See: [[Node - Introduction to Node.js]]

--- 

* Data is NOT sent to the server in its original form 
	* Data requires some processing
* Servers DO NOT wait until all data is received to begin processing
	* This would create a bottleneck & waste a lot of time
* Requests are processed using the following logic
	1) Data is broken down into smaller packages (called streams)
		* Each package is treated separately
	2) An event handler 'listens' for packages
		* Each package is added to the one before it by the **req.on()** method (see [[Node.js - The Request Object]])
			* Data comes in binary code (can be read using the **buffer** object)
	3) Server begins working on packages received while waiting for other packages

##### What are streams? (see [[Node.js - Streams for Reading & Writing Files]])
* A **stream** --> a sequence of data coming from some source
	* Data is transmitted in chunks of 64 KB



