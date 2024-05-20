# What is a DDoS Attack?
* [Video: What is a DDoS Attack?](https://www.cloudflare.com/learning/ddos/what-is-a-ddos-attack/)
* A type of brute force attack (see [[Brute Force]]) where a distributed network of computing resources to attack a website, overwhelming it with sheer numbers and, as a result, debilitating it by consuming all of its bandwidth.

#### Protecting against DDoS Attacks
* Use an [express-rate-limiter](https://www.npmjs.com/package/express-rate-limit) middleware to limit the number of requests from one IP address at one time (see [[Express.js - Module - express-rate-limit]])
```js
const express = require('express');
const rateLimit = require('express-rate-limit');

const app = express();

const limiter = rateLimit({
	windowMs: 15 * 60 * 1000, // in 15 minutes
	max: 100 // you can make a maximum of 100 requests from one IP
});

// applying the rate-limiter
app.use(limiter); 
```