Resources / Additional Reads
* [We’re Under Attack! 23+ Node.js Security Best Practices](https://medium.com/@nodepractices/were-under-attack-23-node-js-security-best-practices-e33c146cb87d)
* [Production Best Practices: Security (including Helmet)](https://expressjs.com/en/advanced/best-practice-security.html)
* [Node.js Security Checklist](https://blog.risingstack.com/node-js-security-checklist/)
* [How to Protect Your Passwords: The Dangers of Plain Text Storage](https://medium.com/practicum-bootcamp/how-to-protect-your-passwords-the-dangers-of-plain-text-storage-b8d63f40c211)

---
### 1) Set the Response Headers
* Can be set manually (see [[Cross-Site Scripting (XSS)]])
* Can be set automatically using the helmet module (see [[Node.js - Module - helmet]])

### 2) Check User Data
* Validate input data and replace control characters with entities using the escape-html module (see [[Cross-Site Scripting (XSS)]], [[Node.js - Module - escape-html]])

### 3) Think About Where Data is Stored on Client Side
* JavaScript can access localStorage and behavior cannot be restricted (see [[Local Storage]])
* Cookies are better suited for storing sensitive data (see [[Cookies]])

### 4) Remember CSRF
* If using cookies, implement protection again CSRF
	* The `SameSite` option will help (see [[Cross-Site Request Forgery (CSRF)]])

### 5) Be Prepared for Brute Force & DDoS Attacks
* Use the express-rate-limit middleware to protect against DDoS Attacks (see [[Distributed Denial of Service (DDoS)]], [[Express.js - Module - express-rate-limit]])
	* Limits the number of requests that a single IP address can make, making attacks that rely on brute force less feasible.

### 6) Check the Dependencies
* Check for dependencies before sending a project to production 
* Set up dependabot on GitHub (see [[Web Security When Using External Libraries & Components]])
```bash
npm run audit
```
