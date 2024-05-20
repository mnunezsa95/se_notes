What is Asynchronous JavaScript? (see [[JS - Synchronous vs Asynchronous]])

* The **Event Loop** --> allows for Asynchronous JS to work
	* Looks into the call stack and determines if empty
		* **if empty** --> takes the first callback from **microtask queue** or **callback queue** and place it on the call stack (called an event loop tick)
			* Microtasks have priority over callback queue
		* **If not empty** --> will wait for it to become empty
	* The microtask or callback is executed
	* The microtask or callback is removed
![](https://lh3.googleusercontent.com/KbsaqVPPA3ZgTYpSsxU2jYqZBauhwitHee7Cz83nCF6XhlRBuZtdtIzg67AWNUd0JUiyRTMtqeENjeKn8Qe2bN4klgYKYv3MWx-BlAlBh6uC-RVaKD6jIIXXug1W5D_7vFY0RKnowXUOTjOvbYw7CeI)

* Asynchronous tasks will run in the web API's environment of the browser
**![](https://lh4.googleusercontent.com/jfKkfDR6HpIP6iV0D8a2n29Dhk9QE-tOmsdPuoIWfVXkhq31jZH3FofZMwxmIXCPM-9LWiK-hvI8fMf7yMEZnihhqXqSSYRDQo-1sWEpnH8zOj16papU2iY6V2mmSMiW25m78oaKu2_-Qta0IXBZgaA)**
