See [[Py - Introduction to Python]], [[What is SMTP?]]
Documentation
* [SMTP Protocol Client (Official)](https://docs.python.org/3/library/smtplib.html)

---
* Python has a built-in module (`smtplib`) which can be used to send emails

#### Importing `smtplib`
```python
import smtplib 
```

#### Using `smtplib`
1) Using the `with` keyword, create an instance of the `SMTP()` class. Pass in the host_server for the email
	* Gmail --> `"smtp.gmail.com"`
	* Yahoo --> `"smtp.yahoo.com"`
2) `starttls()` --> secures connection to email server
3) `login(user= , password= )` --> logins into the email (that will send the email)
4) `sendmail(from_addr= , to_addrs= , msg= )` --> sends the msg from the specified address, to the specified address
```Python
with smtplib.SMTP(host_server) as connection: # creating a connection to gmail
  connection.starttls() # securing connection to email server
  connection.login(user=my_email, password=password)
  connection.sendmail(
    from_addr=my_email
    to_addrs="marlonnunez.dev@gmail.com"
    msg="Subject:Hello, Marlon!\n\nThis is the body of my email"
  )
```

#### Troubleshooting
* The code above might throw an error, if so, follow steps to trouble shoot
	* Sign in to gmail
	* Enable 2-step verification
	* Add an "App password"
	* Copy password, and use as the password for the `login()` method