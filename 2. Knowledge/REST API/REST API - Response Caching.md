* What is Caching? --> Storing data on the client-side 
	* Prevents repetitive requests (see [[REST API - Introduction to REST API]])
# Default Caching Behavior
* GET requests are cached by browser
* POST requests are NOT cached by browser
* PUT, PATCH, and DELETE are not cached at all

--- 
# Caching Headers
* GET and POST can use special caching headers to cache data
* Caching can be done on 
	1) the client-side 
	2) proxy-servers
* 4 Caching headers
	1) Expires
	2) Cache-Control
	3) ETag
	4) Last-Modified
* Caching is set with the **res.header()** method (see [[Express.js - Methods & Properties]])

### Expires Header (client-side)
* Used to indicate a timeframe for the cached data to remain valid. 
	* When the time ends: data will need to be requested from the server again --> cache is updated
* Example
```bash 
# Using the Expires Header
Expires: Fri, 20 May 2016 19:20:49 IST
```

### Cache-Control Header (client-side)
* Used to indicate a **directive** for handling cached data

Most used cached-control headers (for client-side)

| header          | description                                                                                                    |
| --------------- | -------------------------------------------------------------------------------------------------------------- |
| only-if-cached  | if response is in the cache, it will be returned from the cache; if not, browser responds with 504 error       |
| no-cache        | browser makes a conditional validation request to server; if there are changes on server, the cache is updated |
| max-age=30000   | maximum time (in seconds) during which a resource is considered valid                                          |
| must-revalidate | if cache is expired, a request is sent to check the data in the cache                                          |
| no-store        | cache is disabled entirely                                                                                                               |

* Example(s):
```bash
# cache control
Cache-Control: only-if-cached 
Cache-Control: no-cache

# max-age management
Cache-Control: max-age=30000 

# cache update management
Cache-Control: must-revalidate 

# other
Cache-Control: no-store

# indicating serveral headers 
Cache-Control: max-age=30000, must-revalidate 
```

### Cache-Control Header (proxy-servers)

Most used cached-control headers (proxy-server)

| header            | description                                                                  |
| ----------------- | ---------------------------------------------------------------------------- |
| private           | data can ONLY be cached on client-side (does not allow proxy-server caching) |
| public            | data can be stored on proxy-server                                           |
| proxy-revalidate  | data can be stored on proxy-server, but must check if relevant before using  |
| no-transformation | proxies cannot apply changes to the resource                                                                             |

### ETag Header 
* Uses a hashing mechanism to avoid sending the entire cache to server during each validation process
	* Algorithm: Analyzes the cache --> creates a hash (string) --> hash passed through validation 
* Example
```bash
# the string is a hash (unique to the dataset)
ETag: "abcd1234567n34jv"
```

### Last-Modified Header 
* Stores the date that the data was last updated on server
	* Data is validated using date
* Example
```bash
# date of last modified
Last-Modified: Fri, 10 May 2016 09:17:49 IST
```

--- 
# Default Express Cache Behavior
By Default, express:
1) Creates an ETag response header (sent in every response)
2) Browser remembers the value (hash)
3) At next request, another ETag is sent (inside another header called:   **If-None-Match**   )
	* If value of (   If-None-Match   ) matches some cache on server, the response will be 304 - Not Modified and browser takes a cached response (see [[Server Response Status Codes]])
	* If value of (   If-None-Match   ) does not match any cache on server, a new response is sent
