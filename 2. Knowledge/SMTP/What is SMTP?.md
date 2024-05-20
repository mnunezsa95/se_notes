

#### What is Simple Mail Transfer Protocol (SMTP)?
* SMTP (Simple Mail Transfer Protocol) is a [TCP/IP](https://www.techtarget.com/searchnetworking/definition/TCP-IP) protocol used in sending and receiving email. 
* SMTP is used most commonly by email clients, including Gmail, Outlook, Apple Mail and Yahoo Mail.
* SMTP can send and receive email, but email clients typically use a program with SMTP for sending email

#### What is an SMTP server?
* An SMTP server is an application or computer that sends, receives and relays email. These servers typically use TCP on [port](https://www.techtarget.com/searchnetworking/definition/port-number) 25 or 587.
	* The port number identifies specific processes when an internet or network message is forwarded to a server.
* SMTP servers are set to an always-on listening mode and as soon as a server detects a TCP connection from a client, the SMTP process initiates a connection to port 25 to send the email.

#### How SMTP works
1) An email server uses SMTP to send a message from an email client to another email server.
2) The email server uses SMTP as a relay service to send the email to the receiving email server.
3) The receiving email server uses an email client to download incoming mail via IMAP, for example, and places it in the recipient's inbox.

