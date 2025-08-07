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

## 4. XML External Entity

<img width="600" height="315" alt="image" src="https://github.com/user-attachments/assets/425ac476-db69-4dc2-80fe-771b7e2c8213" />

An XML External Entity (XXE) attack is a vulnerability that abuses features of XML parsers/data. It often allows an attacker to interact with any backend or external systems that the application itself can access and can allow the attacker to read the file on that system. They can also cause Denial of Service (DoS) attack or could use XXE to perform Server-Side Request Forgery (SSRF) inducing the web application to make requests to other applications. XXE may even enable port scanning and lead to remote code execution.

#### There are two types of XXE attacks: in-band and out-of-band (OOB-XXE).
1. An **in-band XXE** attack is the one **in which the attacker can receive an immediate response to the XXE payload.**
2. **out-of-band XXE** attacks (also called blind XXE), there is **no immediate response from the web application** and **attacker has to reflect the output of their XXE payload to some other file or their own server.**

#### Before we move on to learn about XXE exploitation we'll have to understand XML properly.

#### What is XML?

XML (eXtensible Markup Language) is a markup language that defines a set of rules for encoding documents in a format that is both human-readable and machine-readable. It is a markup language used for storing and transporting data. 

#### Why we use XML?

1. XML is platform-independent and programming language independent, thus it can be used on any system and supports the technology change when that happens.
2. The data stored and transported using XML can be changed at any point in time without affecting the data presentation.
3. XML allows validation using DTD and Schema. This validation ensures that the XML document is free from any syntax error.
4. XML simplifies data sharing between various systems because of its platform-independent nature. XML data doesn’t require any conversion when transferred between different systems.

#### Syntax

Every XML document mostly starts with what is known as XML Prolog.

```<?xml version="1.0" encoding="UTF-8"?>```


Above the line is called XML prolog and it specifies the XML version and the encoding used in the XML document. This line is not compulsory to use but it is considered a `good practice` to put that line in all your XML documents.

Every XML document must contain a `ROOT` element. For example:

```
<?xml version="1.0" encoding="UTF-8"?>
<mail>
   <to>falcon</to>
   <from>feast</from>
   <subject>About XXE</subject>
   <text>Teach about XXE</text>
</mail>
```


In the above example the ```<mail>``` is the ROOT element of that document and ```<to>, <from>, <subject>, <text>``` are the children elements. If the XML document doesn't have any root element then it would be considered ```wrong or invalid``` XML doc.

Another thing to remember is that XML is a case sensitive language. If a tag starts like ```<to> then it has to end by </to>``` and not by something like </To>(notice the capitalization of T)

Like HTML we can use attributes in XML too. The syntax for having attributes is also very similar to HTML. For example:
```<text category = "message">You need to learn about XXE</text>```

In the above example category is the attribute name and message is the attribute value.

#### Before we move on to start learning about XXE we'll have to understand what is DTD in XML.

**DTD** stands for **Document Type Definitio**n. **A DTD defines the structure and the legal elements and attributes of an XML document.**

Let us try to understand this with the help of an example. Say we have a file named ```note.dtd``` with the following content:

```
<!DOCTYPE note [ <!ELEMENT note (to,from,heading,body)> <!ELEMENT to (#PCDATA)> <!ELEMENT from (#PCDATA)> <!ELEMENT heading (#PCDATA)> <!ELEMENT body (#PCDATA)> ]>
```
Now we can use this DTD to validate the information of some XML document and make sure that the XML file conforms to the rules of that DTD.
Ex: Below is given an XML document that uses note.dtd
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE note SYSTEM "note.dtd">
<note>
    <to>falcon</to>
    <from>feast</from>
    <heading>hacking</heading>
    <body>XXE attack</body>
</note>
```

So now let's understand how that DTD validates the XML. Here's what all those terms used in note.dtd mean

- !DOCTYPE note -  Defines a root element of the document named note
- !ELEMENT note - Defines that the note element must contain the elements: "to, from, heading, body"
- !ELEMENT to - Defines the to element to be of type "#PCDATA"
- !ELEMENT from - Defines the from element to be of type "#PCDATA"
- !ELEMENT heading  - Defines the heading element to be of type "#PCDATA"
- !ELEMENT body - Defines the body element to be of type "#PCDATA"

**NOTE:** #PCDATA means parseable character data.

#### Now we'll see some XXE payload and see how they are working.

1. The first payload we'll see is very simple. If you've read the previous task properly then you'll understand this payload very easily.
```
<!DOCTYPE replace [<!ENTITY name "feast"> ]>
 <userInfo>
  <firstName>falcon</firstName>
  <lastName>&name;</lastName>
 </userInfo>
```

As we can see we are defining a ENTITY called name and assigning it a value feast. Later we are using that ```ENTITY``` in our code.

2. We can also use XXE to read some file from the system by defining an `ENTITY` and having it use the `SYSTEM` keyword

```
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

Here again, we are defining an `ENTITY` with the name read but the difference is that we are setting it value to `SYSTEM` and path of the file.

If we use this payload then a website vulnerable to XXE(normally) would display the content of the file `/etc/passwd`.

In a similar manner, we can use this kind of payload to read other files but a lot of times you can fail to read files in this manner or the reason for failure could be the file you are trying to read.

#### Now let us see some payloads in action. The payload that I'll be using is the one we saw in the previous task.

1) Let's see how the website would look if we'll try to use the payload for displaying the name.

<img width="1445" height="374" alt="image" src="https://github.com/user-attachments/assets/fc1d48e7-3ae7-4df0-a635-33502d6964bd" />

On the left side, we can see the burp request that was sent with the URL encoded payload and on the right side we can see that the payload was able to successfully display name `falcon feast`

2) Now let's try to read the `/etc/passwd`
<img width="1609" height="408" alt="image" src="https://github.com/user-attachments/assets/bfa86865-2823-4210-9a13-3dcc69a5352c" />

## 5. Broken Access Control

<img width="856" height="448" alt="image" src="https://github.com/user-attachments/assets/ed9d98f2-e1d9-4147-8829-0735935524b3" />

Websites have pages that are protected from regular visitors, for example only the site's admin user should be able to access a page to manage other users. **If a website visitor is able to access the protected page/pages that they are not authorised to view, the access controls are broken.**

#### A regular visitor being able to access protected pages, can lead to the following:
- Being able to view sensitive information
- Accessing unauthorized functionality

#### OWASP have a listed a few attack scenarios demonstrating access control weaknesses:

#### Scenario #1: 
The application uses unverified data in a SQL call that is accessing account information:
```
pstmt.setString(1, request.getParameter("acct"));
ResultSet results = pstmt.executeQuery( );
```

An attacker simply modifies the ‘acct’ parameter in the browser to send whatever account number they want. If not properly verified, the attacker can access any user’s account.
`http://example.com/app/accountInfo?acct=notmyacct`

#### Scenario #2: 
An attacker simply force browses to target URLs. Admin rights are required for access to the admin page.
```
http://example.com/app/getappInfo
http://example.com/app/admin_getappInfo
```

If an unauthenticated user can access either page, it’s a flaw. If a non-admin can access the admin page, this is a flaw (reference to scenarios).

#### To put simply, broken access control allows attackers to bypass authorization which can allow them to view sensitive data or perform tasks as if they were a privileged user.

<img width="571" height="341" alt="image" src="https://github.com/user-attachments/assets/1a98c816-30e2-4ac7-9027-bb2135edf3f6" />

**IDOR, or Insecure Direct Object Reference**, is the **act of exploiting a misconfiguration** in the way user input is handled, to access resources you wouldn't ordinarily be able to access. **IDOR is a type of access control vulnerability**.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this `https://example.com/bank?account_number=1234`. On that page we can see all our important bank details, and a user would do whatever they needed to do and move along their way thinking nothing is wrong.

There is however a potentially huge problem here, **a hacker may be able to change the account_number parameter to something else like 1235, and if the site is incorrectly configured, then he would have access to someone else's bank information**.

## 6. Security Misconfiguration

Security Misconfigurations are distinct from the other Top 10 vulnerabilities, because they occur when security could have been configured properly but was not.

Security misconfigurations include:

- Poorly configured permissions on cloud services, like S3 buckets
- Having unnecessary features enabled, like services, pages, accounts or privileges
- Default accounts with unchanged passwords
- Error messages that are overly detailed and allow an attacker to find out more about the system
- Not using [HTTP security headers](https://owasp.org/www-project-secure-headers/), or revealing too much detail in the Server: HTTP header

This vulnerability can often lead to more vulnerabilities, such as default credentials giving you access to sensitive data, XXE or command injection on admin pages.

For more info, I recommend having a look at the [OWASP top 10 entry for Security Misconfiguration](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A6-Security_Misconfiguration)

### Default Passwords
Specifically, this VM focusses on default passwords. These are a specific example of a security misconfiguration. You could, and should, change any default passwords but people often don't.

It's particularly common in embedded and Internet of Things devices, and much of the time the owners don't change these passwords.

It's easy to imagine the risk of default credentials from an attacker's point of view. Being able to gain access to admin dashboards, services designed for system administrators or manufacturers, or even network infrastructure could be incredibly useful in attacking a business. From data exposure to easy RCE, the effects of default credentials can be severe.

**In October 2016, Dyn (a DNS provider) was taken offline by one of the most memorable DDoS attacks of the past 10 years. The flood of traffic came mostly from Internet of Things and networking devices like routers and modems, infected by the Mirai malware.**

How did the malware take over the systems? Default passwords. The malware had a list of 63 username/password pairs, and attempted to log in to exposed telnet services.

The DDoS attack was notable because it took many large websites and services offline. Amazon, Twitter, Netflix, GitHub, Xbox Live, PlayStation Network, and many more services went offline for several hours in 3 waves of DDoS attacks on Dyn.

## 7. Cross-site Scripting

### XSS Explained
Cross-site scripting, also known as XSS is a security vulnerability typically found in web applications. It’s a type of injection which can allow an attacker to execute malicious scripts and have it execute on a victim’s machine.

#### A web application is vulnerable to XSS if it uses unsanitized user input. XSS is possible in Javascript, VBScript, Flash and CSS. There are three main types of cross-site scripting:
- **Stored XSS** - the most dangerous type of XSS. This is where a malicious string originates from the website’s database. This often happens when a website allows user input that is not sanitised (remove the "bad parts" of a users input) when inserted into the database.
- **Reflected XSS** - the malicious payload is part of the victims request to the website. The website includes this payload in response back to the user. To summarise, an attacker needs to trick a victim into clicking a URL to execute their malicious payload.
- **DOM-Based XSS** - DOM stands for Document Object Model and is a programming interface for HTML and XML documents. It represents the page so that programs can change the document structure, style and content. A web page is a document and this document can be either displayed in the browser window or as the HTML source.

### XSS Payloads
Remember, cross-site scripting is a vulnerability that can be exploited to execute malicious Javascript on a victim’s machine. Check out some common payloads types used:
- **Popup's (<script>alert(“Hello World”)</script>)** - Creates a Hello World message popup on a users browser.
- **Writing HTML (document.write)** - Override the website's HTML to add your own (essentially defacing the entire page).
- **Port scanning (http://www.xss-payloads.com/payloads/scripts/portscanapi.js.html)** - A mini local port scanner (more information on this is covered in the TryHackMe XSS room).
- **XSS Keylogger: (http://www.xss-payloads.com/payloads/scripts/simplekeylogger.js.html)** - You can log all keystrokes of a user, capturing their password and other sensitive information they type into the webpage.

**XSS-Payloads.com (http://www.xss-payloads.com/) ]** - is a website that has XSS related Payloads, Tools, Documentation and more. You can download XSS payloads that take snapshots from a webcam or even get a more capable port and network scanner.
