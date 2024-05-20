Resources:
* Udemy Video: How the Web Works: Requests & Responses](https://www.udemy.com/course/the-complete-javascript-course/learn/lecture/22649297#overview)

---
### Creator of the World Wide Web
* Tim Berners-Lee (1991)
### Important Definitions
* HTTP -- HyperText Transfer Protocol
* HTTPW -- HyperText Transfer Protocol Secure
* Domain -- an easy-to-remember address for a website
* DNS -- a special server that acts like a phonebook
* Real address
	* Protocol --> HTTP or HTTPS
	* IP Address --> the actual address
	* Port --> 
		* 443 for https
		* 80 for http
* TCP (transmission control protocol)
* IP (internet protocol)

### How it works
1)  The **DOMAIN** (e.g. www.someWebsite.com) is not the real address
1) The **DNS** will match the domain to the real IP address (through internet server provider)
2) The TCP/IP socket connection is established (Client --> <-- Server)
	* Communication protocol that defines how data travels
3) HTTP Request is sent (Client --> Server) (see [[Node.js - The Request Object]])
	* Contains info such as 
		* Method
		* Request headers
		* Request body
4) HTTP Response (Client <-- Server) (see [[Node.js - The Response Object]])
	* Contains info such as
		* Response start line (status code & status message)
		* Response headers
		* Response body


