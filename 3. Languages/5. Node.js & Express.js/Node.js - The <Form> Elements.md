See: [[Node - Introduction to Node.js?]]

--- 

* The < From > element attributes change how data is sent to the server (when submitted via HTML)
##### Form Attributes
| Attribute | Description                                                    |                            
| --------- | -------------------------------------------------------------- | -------------------------- |
| action    | the URL/path to send the request to                            | 
| method    | the HTTTP method to use when submitting the form (e.g. 'post') | 'put' 'delete' not support |              
| enctype   | the encoding type of the request body (e.g. 'text/plain')      | defaut 'application/x-www-form-urlencoded' |

```html
<form action="/submit" method="post" enctype="text/plain"> 
	... 
</form>
```
