# OWASP Top 10:2017
This breaks each **OWASP** topic down and includes details on what the vulnerability is, how it occurs and how you can exploit it. You will put the theory into practise by completing supporting challenges.
- **Injection**
- **Broken Authentication**
- **Sensitive Data Exposure**
- **XML External Entity**
- **Broken Access Control**
- **Security Misconfiguration**
- **Cross-site Scripting**
- **Insecure Deserialization**
- **Components with Known Vulnerabilities**
- **Insufficent Logging & Monitoring**

## 1. Injection
Injection flaws are very common in applications today. These flaws occur because user controlled input is interpreted as actual commands or parameters by the application. Injection attacks depend on what technologies are being used and how exactly the input is interpreted by these technologies. 

#### Some common examples include:
- **SQL Injection:** This occurs when user controlled input is passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries. 
- **Command Injection:** This occurs when user input is passed to system commands. As a result, an attacker is able to execute arbitrary system commands on application servers.

#### If an attacker is able to successfully pass input that is interpreted correctly, they would be able to do the following:
- Access, Modify and Delete information in a database when this input is passed into database queries. This would mean that an attacker can steal sensitive information such as personal details and credentials.
- Execute Arbitrary system commands on a server that would allow an attacker to gain access to users’ systems. This would enable them to steal sensitive data and carry out more attacks against infrastructure linked to the server on which the command is executed.

#### The main defence for preventing injection attacks is ensuring that user controlled input is not interpreted as queries or commands. There are different ways of doing this:
- **Using an allow list:** when input is sent to the server, this input is compared to a list of safe input or characters. If the input is marked as safe, then it is processed. Otherwise, it is rejected and the application throws an error.
- **Stripping input:** If the input contains dangerous characters, these characters are removed before they are processed.

**NOTE:** Dangerous characters or input is classified as any input that can change how the underlying data is processed. Instead of manually constructing allow lists or even just stripping input, there are various libraries that perform these actions for you.

## 2. Broken Authentication
Authentication and session management constitute core components of modern web applications. Authentication allows users to gain access to web applications by verifying their identities. The most common form of authentication is using a username and password mechanism. A user would enter these credentials, the server would verify them. If they are correct, the server would then provide the users’ browser with a session cookie. A session cookie is needed because web servers use HTTP(S) to communicate which is stateless. Attaching session cookies means that the server will know who is sending what data. The server can then keep track of users' actions. 

If an attacker is able to find flaws in an authentication mechanism, they would then successfully gain access to other users’ accounts. This would allow the attacker to access sensitive data (depending on the purpose of the application). 

#### Some common flaws in authentication mechanisms include:
- **Brute force attacks:** If a web application uses usernames and passwords, an attacker is able to launch brute force attacks that allow them to guess the username and passwords using multiple authentication attempts. 
- **Use of weak credentials:** web applications should set strong password policies. If applications allow users to set passwords such as ‘password1’ or common passwords, then an attacker is able to easily guess them and access user accounts. They can do this without brute forcing and without multiple attempts.
- **Weak Session Cookies:** Session cookies are how the server keeps track of users. If session cookies contain predictable values, an attacker can set their own session cookies and access users’ accounts. 

#### There can be various mitigation for broken authentication mechanisms depending on the exact flaw:
- To avoid password guessing attacks, ensure the application enforces a **strong password policy**. 
- To **avoid brute force attacks**, ensure that the application **enforces an automatic lockout after a certain number of attempts**. This would prevent an attacker from launching more brute force attacks.
- **Implement Multi Factor Authentication** - If a user has multiple methods of authentication, for example, using username and passwords and receiving a code on their mobile device, then it would be difficult for an attacker to get access to both credentials to get access to their account.

## 3. Sensitive Data Exposure 
**When a webapp accidentally divulges sensitive data**, we refer to it as **"Sensitive Data Exposure"**. This is often **data directly linked to customers (e.g. names, dates-of-birth, financial information, etc)**, but could also be more technical information, such as **usernames and passwords**. At more complex levels this often involves techniques such as a **"Man in The Middle Attack"**, whereby the attacker would force user connections through a device which they control, then **take advantage of weak encryption** on any **transmitted data to gain access** to the intercepted information (if the data is even encrypted in the first place...). Of course, many examples are much simpler, and vulnerabilities can be found in web apps which can be exploited without any advanced networking knowledge. Indeed, in some cases, the sensitive data can be found directly on the webserver itself...

The **most common way to store a large amount of data in a format that is easily accessible from many locations at once is in a database.** This is obviously perfect for something like a web application, as there may be many users interacting with the website at any one time. **Database engines usually follow the Structured Query Language (SQL) syntax; however, alternative formats (such as NoSQL) are rising in popularity.**

In a production environment it is common to see databases set up on dedicated servers, running a database service such as MySQL or MariaDB; however, databases can also be stored as files. These databases are referred to as "flat-file" databases, as they are stored as a single file on the computer. This is much easier than setting up a full database server, and so could potentially be seen in smaller web applications. Accessing a database server is outwith the scope of today's task, so let's focus instead on flat-file databases.

As mentioned previously,**flat-file databases are stored as a file on the disk of a computer.** Usually this would not be a problem for a webapp, but what happens **if the database is stored underneath the root directory of the website** (i.e. one of the files that a user connecting to the website is able to access)? **Well, we can download it and query it on our own machine, with full access to everything in the database. Sensitive Data Exposure indeed!**

That is a big hint for the challenge, so let's briefly cover some of the syntax we would use to query a flat-file database.

**The most common (and simplest) format of flat-file database is an sqlite database.** These can be interacted with in most programming languages, and have a dedicated client for querying them on the command line. **This client is called "sqlite3", and is installed by default on Kali.**

#### Let's suppose we have successfully managed to download a database:

<img width="603" height="89" alt="image" src="https://github.com/user-attachments/assets/eb7d6315-e724-483a-843c-a0802a625d22" />

#### We can see that there is an SQlite database in the current folder.

To access it we use: ```sqlite3 <database-name>:```

<img width="405" height="79" alt="image" src="https://github.com/user-attachments/assets/2203dbb1-835f-4434-94f1-a09c2beb7325" />

From here we can see the tables in the database by using the ```.tables``` command:

<img width="406" height="89" alt="image" src="https://github.com/user-attachments/assets/d84520e3-ac99-4fd7-a66e-95b6087d8cc8" />

**At this point we can dump all of the data from the table,** but we won't necessarily know what each column means unless we look at the table information. First let's use ```PRAGMA table_info(customers);``` to see the table information, then we'll use ```SELECT * FROM customers;``` to dump the information from the table:

<img width="561" height="217" alt="image" src="https://github.com/user-attachments/assets/34993887-cbba-4c4a-a44e-b99ecd5d2ec9" />

We can see from the table information that there are **four columns: custID, custName, creditCard and password**. You may notice that this matches up with the results. Take the first row:

```0|Joy Paulson|4916 9012 2231 7905|5f4dcc3b5aa765d61d8327deb882cf99```
 
**We have the custID (0), the custName (Joy Paulson), the creditCard (4916 9012 2231 7905) and a password hash (5f4dcc3b5aa765d61d8327deb882cf99).**

In the previous task we saw how to query an SQLite database for sensitive data. We found a collection of password hashes, one for each user. In this task we will briefly cover how to crack these.

**When it comes to hash cracking,** Kali comes pre-installed with various tools -- if you know how to use these then feel free to do so; however, they are outwith the scope of this material.

Instead we will be using the online tool: **[Crackstation](https://crackstation.net/)**. **This website is extremely good at cracking weak password hashes.** For more complicated hashes we would need more sophisticated tools; however, all of the crackable password hashes used in today's challenge are weak MD5 hashes, which Crackstation should handle very nicely indeed.

#### When we navigate to the website we are met with the following interface:

<img width="1011" height="318" alt="image" src="https://github.com/user-attachments/assets/ca8e1729-48db-4c40-9377-3543594f1d26" />

#### Let's try pasting in the password hash for Joy Paulson which we found in the previous task (5f4dcc3b5aa765d61d8327deb882cf99). We solve the Captcha, then click the "Crack Hashes" button:

<img width="1012" height="395" alt="image" src="https://github.com/user-attachments/assets/6af995b8-abc5-4fc2-89af-a5d6564942d1" />

#### We see that the hash was successfully broken, and that the user's password was "password" -- how secure!

It's worth noting that Crackstation works using a massive wordlist. If the password is not in the wordlist then Crackstation will not be able to break the hash.


