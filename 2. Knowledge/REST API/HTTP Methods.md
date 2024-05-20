# URI
* Resources are accessible via a URI (Uniform Resource Identifier)
	* URIs --> point to a specific resource
*  Example: URI
```bash
https://test.nomoreparties.co/cards/5d1f0611d321eb4bdcd707dd 
# This URI points to a resource that is addressed using its id
```

---
# HTTP Method Types

| HTTP Method | Used for/to:                                        |
| ----------- | --------------------------------------------------- |
| GET         | retrieve data from server                           |
| POST        | create a resource on server                         |
| PUT         | update a resource on server                         |
| PATCH       | apply partial modifications to an existing resource |
| DELETE      | delete a resource on sever                          |
| HEAD        | get a response header w/o the response body         |
| OPTIONS     | describe which HTTP method the server supports      |

* HTTP Methods can be called on:
	* app
	* router Module (see [[Express.js - Routing]])
```js
app.get('/books', getBooks); 
app.post('/books', createBook); 
app.put('/books/:id', replaceBook); 
app.patch('/books/:id', updateBookInfo); 
app.delete('/books/:id', deleteBook);

router.get('/books', getBooks); 
router.post('/books', createBook); 
router.put('/books/:id', replaceBook); 
router.patch('/books/:id', updateBookInfo);
router.delete('/books/:id', deleteBook);
```

# Testing REST API
* REST APIs can be tested using Postman (see [[Server Testing - Postman]])