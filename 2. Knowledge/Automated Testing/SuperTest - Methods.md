* SuperTest Methods can be used to write tests for HTTP requests(see [[SuperTest - Testing HTTP Requests]])
# Checking Request Sending
* For each type of request (get, post, delete, put, patch) there is a method with the same name. 
* For each of these methods, the URL to be check is passed as an argument
#### get()
* Used to test a get request
* Arguments
	* URL --> the url of the request to be checked
* Example
```js
describe('Endpoints respond to requests', () => {
	it('Returns data and status 200 on request to "/"', () => {
		return request.get('/').then((response) => {
	        expect(response.status).toBe(200);
            expect(response.text).toBe('Hello, world!');
        });
	});
}); 
```

#### post()

#### delete() 

#### put()

#### patch()


--- 
#### set() 
* Sets the attributes
* Arguments
	* attributeName
	* attributeValue
* Example
```js
.set('Cookie', ['token=u1a90aw7812689adukqyw61;'])
```

#### send()
* Sets the request body (allows us to add data to the request body)
* Arguments
	* object --> contain key/value pairs to be sent as info
* Example
```js
send({name: "Mr. Pink"})
```

#### query()
* Allows us to configure a GET request, which doesn't have a body, ONLY a URL.
	* To add data to this URL, pass the data as an object, as an argument
* Arguments
	* object --> contains data for the query method
* Example
```js
.query({ per_page: '50', offset: '20' }) 
```

#### attach()
* Used to attach a file to the request
* Arguments
	* filename --> name of the file
	* relativePath --> path to the file
* Example
```js
.attach('avatar', 'test/fixtures/avatar.jpg') 
```

