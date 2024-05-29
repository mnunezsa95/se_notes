Resources
* [Checking for Node.js Compatibility](https://kangax.github.io/compat-table/es6/)
	* A compatibility table that shows whether or not Node.js supports a certain functionality.
* Official [Node.js Documentation](https://nodejs.org/docs/latest-v18.x/api/index.html)

---

## What is Node.JS?
* Made from 2 components
	1) A JavaScript Engine (uses the Chrome V8 engine)
		* Compiles and executes code (like a browser) [[Node.js - Entering Node.js Mode]]
	2) A set of modules
		* Allow JavaScript to interact w/ computer systems (file system, network, etc)

## How does Node.js work?
* Servers have a Network Interface Card (NIC) --> accept requests coming from the network
	* NIC must be accessed to process requests & exchange data
* JS alone cannot receive data from NIC 
	* JS does not have built-in functionality for interacting w/ hardware
* Node.js uses a library of commands (in another language) that do have functionality
	* JavaScript Modules allow JS to work with the **libuv library** (written in C), which allows JS to work with the NIC
		* Libuv is a library of commands that have JavaScript functions attached to it

**![](https://lh4.googleusercontent.com/_-dG3OhJiZL6nBNZ3jwQoc1LL-6pDKCPr1N06CyqA8Dk1Te3fadSLDjyE9gmuVCswFXLhHJJMWHueSjCNZbN420K2IzSv8kdpNEnLvHSeZv8BLEAvsAeVrB9xjHKlkdfigjpXNdVHRXB-7prZy7uGm4)**

