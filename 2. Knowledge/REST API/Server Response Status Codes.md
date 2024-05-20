
## The Server Response
* Server responses **ALWAYS** contain a status code

## Status Code Categories
* Status Codes are divided into 5 categories. Requests start with one of the following numbers:

| Category                    | Category Description Indicates                                                                             |
| --------------------------- | ---------------------------------------------------------------------------------------------------------- |
| 1xx: Informational response | request was received by server, client must wait for final response                                        |
| 2xx: Success response       | request was successful                                                                                     |
| 3xx: Redirection            | request has been redirected to another server; client must take further action to complete request         |
| 4xx: Client Error           | Error on the client-side; request was either not generated correctly or client does not have access rights |
| 5xx: Sever Error            | Error on server-side; something has broken or server is overloaded                                         |

## Common Status Codes
Resource: [Complete List of Status Code](https://restfulapi.net/http-status-codes/)

| Response | Name                   | Description:                                                                           |
| -------- | ---------------------- | -------------------------------------------------------------------------------------- |
| 200      | OK                     | The GET request was successful                                                         |
| 201      | Created                | The POST request was successful (resource was created on server)                       |
| 202      | Accepted               | The server started processing the request (but has not finished)                       |
| 301      | Move Permanently       | Resource has moved to a new URI                                                        |
| 302      | Found                  | Request must be re-directed to a different URI; location header should provide new URL |
| 400      | Bad Request            | Generic status for client-side error (sent when other 4xx responses do not fit)        |
| 401      | Unauthorized           | Request requires authorization (authorization is missing or malformed)                 |
| 403      | Forbidden              | Request is correct, but client does not have access rights                             |
| 404      | Not Found              | Resource was NOT found                                                                 |
| 405      | Method Not Allowed     | Requested resource does not support HTTP method used to make the request               |
| 500      | Internal Service Error | Generic status for server-side errors (not the client's fault)                         |
| 501      | Not Implemented        | Resource is on server, but request is NOT supported by the server                      |
| 502      | Bad Gateway            | Error in exchanging data between servers                                               |
| 503      | Servers Unavailable    | Server is temporarily unable to process requests                                       |

# Setting the Status Code
* The status() method of the response object is used to set the response (see [[Express.js - Methods & Properties]]) 
