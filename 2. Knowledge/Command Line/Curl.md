# What is Curl?
* Client URL (cURL, pronounced “curl”) is a command line tool that enables data exchange between a device and a server through a terminal
* Curl is a utility that sends HTTP or HTTPS requests

# Using Curl
1) Open up command line (or vsCode terminal)
2) Curl commands start with "curl", followed by the command

```bash
# sends a GET request to the URL
curl requestURL

# semicolon indicates the beginning of a new line
# echo w/o any arguments prints a new line on the terminal
curl requestURL ; echo

# the capital -X flag allows us to specify the method for curl to use
curl -X "PATCH" requestURL ; echo
curl -C "DELETE" requestURL ; echo
```
