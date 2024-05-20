See: [[Node - Introduction to Node.js?]], [[Express - Introduction to Express.js]]

---

After setting up an Express server --> configure routing settings (see [[Express.js - Creating an Express App]])

# Requests
The **request** contains info about what the user needs
* The request is structured differently depending on the request received
	* GET requests --> a string
		* Requests are stored in the query property of the req object (see [[Express.js - Methods & Properties]])
* What is a query string?
	* A string with name-value pairs separated by ampersands (appended to a URL)
	* Example(s)
		* https://service.example.com/register?username=super+webdev&email=superwebdev@practicum.com&password=12345678
			* Names --> username, email and password
			* Values --> super webdev, superwevdev@practicum.com, and 12345678 
		* `${BASE_PATH}/pokemon?type=fire&stage=3`;
			* URL --> ${BASE_PATH}/pokemon
			* Names --> type, stage
			* Values --> fire, 3

# Responses
* The response contains data that will be sent to the user using the res.send() method (see [[Express.js - Methods & Properties]])


