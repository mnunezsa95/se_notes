
## REST API (Representational State Transfer API) 
* REST is a set of conventions for building an API
	* APIs built with REST principals are called 'REST APIs'
* REST APIs use two sides, which are independent
	* a client 
	* a server

#### REST Principals
* Have made it possible to separate the client from the server, which has:
	1) Made it easier to adapt an application to various platforms
	2) Possible to create public APIs
	3) Easier and faster to build and test server software
#### Contraints to REST
* Most APIs are not 100% REST compliant
	* But follow most REST conventions
* There are 6 REST Principals

--- 
# REST Principles
#### 1. Client-Server Communication
* The Server and Client should be separate
* Interaction between client and server should happen in form of Requests
	* The client makes the request to the server
	* The server stores and sends data
#### 2. Stateless
* The server does NOT store any information about the current session
	* Each request contains all the info needed to process the request
	* Using token authorization, the server does not need to store session info
#### 3. Uniform Interface
* Uniform Interface --> the REST API has a standard and consistent way to access the interface
	* Can be done via the standard HTTP methods and a consistent URL scheme
	* Example
```
/<resource name>/<resource id>
```

* The 4 formal parts of the Uniform Interface definition
	1) Resource Identification in Requests:
		* The request identifies the resource that it wants
			* Example: The request: GET /cards/1  asks for a specific card (the one with an id of 1)
	2) Resource manipulation through representations:
		* Data sent back representing the resource contains enough info to modify or delete the resource
			* Example:  a card resource sent back from the server should include the id, because the card's id tells you where to send a PATCH/PUT/DELETE request for that card, e.g. DELETE /cards/1. 
	3) Self-descriptive messages:
		* Response should include info about how to parse it
			* Example: when sending back JSON data, the response header includes a MIME type indicating that it is JSON
	4) Hypermedia as the engine of application state (HATEOAS):
		* When requesting a resource, the data sent back includes links to other related resources instead of relying on external documentation to discover these related objects
			* Example: A response to GET /cards/1 that conforms to this constraint could embed links within the data like this:
```json
{ 
  card: { 
    id: 1, 
    ...other card attributes... 
  }, 
  links: { 
    owner: "/users/123", 
    likes: "/cards/1/likes" 
  } 
}
```

#### 4. Layered System
* Allows for complex systems that include more servers in the middle of operations, without breaking the first constraint
#### 5. Cacheable
* The Response can be cached
	* Data should be storable on the client side for later retrieval and use
		* Prevents client from unnecessarily requesting the same info over and over
#### 6. Code-on Demand (Optional)
* A server can extend a client's functionality using server code
	* The server sends JavaScript and Client executes it in the browser
