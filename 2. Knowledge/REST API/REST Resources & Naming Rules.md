# REST API  Resources
* What is a REST API (see [[REST API - Introduction to REST API]])
* A **REST API Resource** --> a document, an image, a blog post, a social network user, or anything else that can be accessed with an HTTP request. 
* A **resource** is a conceptual mapping of an object, or set of objects, but NOT the object itself

---
# Naming Rules
1) Use **plural nouns** for resources (especially when targeting a 'collection' of items )
	* **Collection** --> a directory of resources on the server
```bash
# cards and users is the collection
https://nomoreparties.co/users 
https://nomoreparties.co/cards
```

2) Use **single nouns** for single documents (also called document resource)
	* **document resource** --> a singular item inside a resource collection
```bash
# profile is a document
https://nomoreparties.co/users/{user-id}/profile
```

3) Use **verbs** for **controller** resources (see [[MongoDB - Controllers]])
	* **controller** --> collection of executable functions with parameters (inputs) and return values (outputs)
```bash
# checkout is a controller function
https://nomoreparties.co/users/{user-id}/cart/checkout
```

4) Use **forward slash ( / )** to indicate hierarchical relationships
	* DO NOT use a trailing slash (a slash at the end w/ no purpose)
```bash
# using forward slashes for relationships
/users/{user-id}/posts

# DO NOT use trailing slash 
/users/{user-id}/posts/
```

5) Use hyphens or underscores to represent spaces in a URI 
	* Hyphen are preferred (easier to see)
```bash
# do this
/users/{user-id}/user-devices

# do not do this
/users/{user-id}/user_devices 
```

6) User lowercase 
	* URIs are case sensitive (keeps things simple)
```bash
# these are two different URIs:
/users/{user-id}/posts 
/users/{user-id}/Posts
```

7) Do NOT reference HTTP Method in the name
	* avoid naming resources with a reference to the method used
```bash
# do not do this!
/get-users
/create-user

# do this!
/users
/user
```

