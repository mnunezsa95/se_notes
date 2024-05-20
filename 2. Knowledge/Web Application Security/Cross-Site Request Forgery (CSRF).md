# What is an CSRF Attack?
* Based on the fact that along with the HTTP request, the browser sends a cookie to the corresponding domain

# What do CSRF Attacks do?
* CSRF attacks use an authenticated user's cookies to gain access to a site or a site's permissions to perform malicious commands.

#### Protecting against CSRF Attacks
* Tell the browser to only send cookies if the request is from the same domain using the `sameSite` option of the `res.cookie()` method (see [[Cookies]], [[Express.js - Methods & Properties]])
