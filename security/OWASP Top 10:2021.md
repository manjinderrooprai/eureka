# OWASP Top 10:2021

This breaks each OWASP topic down and includes details on what the vulnerability is, how it occurs and how you can exploit it. You will put the theory into practise by completing supporting challenges.

1. **A01:2021 Broken Access Control**
2. **A02:2021 Cryptographic Failures**
3. **A03:2021 Injection**
4. **A04:2021 Insecure Design**
5. **A05:2021 Security Misconfiguration**
6. **A06:2021 Vulnerable and Outdated Components**
7. **A07:2021 Identification and Authentication Failures**
8. **A08:2021 Software and Data Integrity Failures**
9. **A09:2021 Security Logging and Monitoring Failures**
10. **A10:2021 Server-Side Request Forgery (SSRF)** 

### Key Changes from the 2017 List

OWASP introduced notable updates in the 2021 version:

* **Three New Categories Added**:
  * **Insecure Design (A04)**
  * **Software and Data Integrity Failures (A08)**
  * **Server-Side Request Forgery (SSRF) (A10)** 

* **Renamed or Broadened Categories**:
  * *Sensitive Data Exposure* → **Cryptographic Failures (A02)**
  * *Broken Authentication* → **Identification and Authentication Failures (A07)** 

* **Consolidated Categories**:

  * *Cross-Site Scripting (XSS)* is now part of **Injection (A03)**
  * *XML External Entities (XXE)* merged into **Security Misconfiguration (A05)**
  * *Insecure Deserialization* included under **Software and Data Integrity Failures (A08)**

## 1. Broken Access Control

<img width="856" height="448" alt="image" src="https://github.com/user-attachments/assets/f324743b-70f9-457e-b2df-45763ff04b64" />

**Websites have pages that are protected from regular visitors**. For example, **only the site's admin user should be able to access a page to manage other users**. **If a website visitor can access protected pages they are not meant to see, then the access controls are broken**.

#### A regular visitor being able to access protected pages can lead to the following:

- **Being able to view sensitive information from other users**
- **Accessing unauthorized functionality**

Simply put, **broken access control allows attackers to bypass authorisation**, allowing them to **view sensitive data** or **perform tasks they aren't supposed to**.

**For example**, a vulnerability was found in 2019, where an attacker could get any single frame from a Youtube video marked as private. The researcher who found the vulnerability showed that he could ask for several frames and somewhat reconstruct the video. Since the expectation from a user when marking a video as private would be that nobody had access to it, this was indeed accepted as a broken access control vulnerability.

#### Insecure Direct Object Reference

**IDOR or Insecure Direct Object Reference** refers to an **access control vulnerability** where you can access resources you wouldn't ordinarily be able to see. This **occurs when the programmer exposes a Direct Object Reference**, which is just an identifier that refers to specific objects within the server. **By object, we could mean a file, a user, a bank account in a banking application, or anything really**.

For example, let's say we're logging into our bank account, and after correctly authenticating ourselves, we get taken to a URL like this `https://bank.thm/account?id=111111`. On that page, we can see all our important bank details, and a user would do whatever they need to do and move along their way, thinking nothing is wrong.

<img width="805" height="364" alt="image" src="https://github.com/user-attachments/assets/7735001b-6747-4aca-a0b6-e1b237972fd1" />

There is, however, **a potentially huge problem here**, anyone may be able to change the `id` parameter to something else like `222222`, and if the site is incorrectly configured, then he would have access to someone else's bank information.

<img width="805" height="365" alt="image" src="https://github.com/user-attachments/assets/477e14a8-6e1a-4556-b086-ea38a152673b" />

The application exposes a direct object reference through the id parameter in the URL, which points to specific accounts. **Since the application isn't checking if the logged-in user owns the referenced account**, **an attacker can get sensitive information from other users because of the IDOR vulnerability**. Notice that **direct object references aren't the problem**, **but rather that the application doesn't validate if the logged-in user should have access to the requested account**.

#### Prevent Broken Access Control and IDOR:

* Enforce **server-side authorization checks** for every request.
* Verify **both authentication and authorization** before granting access.
* Use **unpredictable identifiers** (UUIDs, random IDs) instead of sequential numbers.
* Implement **Role-Based Access Control (RBAC)** or **Attribute-Based Access Control (ABAC)**.
* Apply the **principle of least privilege**.
* Validate access at all layers — controller, service, and database query level.
* Filter DB queries by **current user’s ownership**.
* Do **not rely on hidden UI elements** or client-side checks for security.
* **Centralize** access control logic in one place.
* Regularly perform **security testing** (manual, automated, penetration testing).

## 2. Cryptographic Failures

A **cryptographic failure** refers to **any vulnerability arising from the misuse (or lack of use) of cryptographic algorithms for protecting sensitive information**. Web applications require cryptography to provide confidentiality for their users at many levels.

#### Take, for example, a secure email application:

* When you are accessing your email account using your browser, you want to be sure that the communications between you and the server are encrypted. That way, any eavesdropper trying to capture your network packets won't be able to recover the content of your email addresses. When we encrypt the network traffic between the client and server, we usually refer to this as **encrypting data in transit**.
* Since your emails are stored in some server managed by your provider, it is also desirable that the email provider can't read their client's emails. To this end, your emails might also be encrypted when stored on the servers. This is referred to as **encrypting data at rest**.

**Cryptographic failures often end up in web apps accidentally divulging sensitive data**. This is often **data directly linked to customers (e.g. names, dates of birth, financial information)**, but it could also be **more technical information, such as usernames and passwords**.

At more complex levels, **taking advantage of some cryptographic failures often involves techniques such as "Man in The Middle Attacks"**, whereby the attacker would force user connections through a device they control. Then, **they would take advantage of weak encryption on any transmitted data to access the intercepted information (if the data is even encrypted in the first place)**. Of course, many examples are much simpler, and vulnerabilities can be found in web apps that can be exploited without advanced networking knowledge. Indeed, in some cases, **the sensitive data can be found directly on the web server itself**.

#### Examples:

The most common way to **store a large amount of data in a format easily accessible from many locations is in a database**. This is perfect for something like a web application, as many users may interact with the website at any time. **Database engines usually follow the Structured Query Language (SQL) syntax**.

In a production environment, it is common to see databases set up on dedicated servers running a database service such as MySQL or MariaDB; **however, databases can also be stored as files**. These are referred to as **"flat-file" databases, as they are stored as a single file on the computer**. This is much easier than setting up an entire database server and could potentially be seen in smaller web applications. Accessing a database server is outwith the scope of today's task, so let's focus instead on flat-file databases.

As mentioned previously, **flat-file databases are stored as a file on the disk of a computer**. Usually, this would not be a problem for a web app, but what happens **if the database is stored underneath the root directory of the website** (i.e. one of the files accessible to the user connecting to the website)? **Well, we can download and query it on our own machine, with full access to everything in the database**. Sensitive Data Exposure, indeed!

That is a big hint for the challenge, so let's briefly cover some of the syntax we would use to query a flat-file database.

The most common (and simplest) format of a flat-file database is an SQLite database. These can be interacted with in most programming languages and have a dedicated client for querying them on the command line. This client is called `sqlite3` and is installed on many Linux distributions by default.

Let's suppose we have successfully managed to download a database:

```
Linux
user@linux$ ls -l 
-rw-r--r-- 1 user user 8192 Feb  2 20:33 example.db
                                                                                                                                                      
user@linux$ file example.db 
example.db: SQLite 3.x database, last written using SQLite version 3039002, file counter 1, database pages 2, cookie 0x1, schema 4, UTF-8, version-valid-for 1
```
We can see that there is an `SQLite database` in the current folder.

To access it, we use `sqlite3 <database-name>`:

```
Linux
user@linux$ sqlite3 example.db                     
SQLite version 3.39.2 2022-07-21 15:24:47
Enter ".help" for usage hints.
sqlite>
```
From here, we can see the tables in the database by using the `.tables` command:

```
Linux
user@linux$ sqlite3 example.db                     
SQLite version 3.39.2 2022-07-21 15:24:47
Enter ".help" for usage hints.
sqlite> .tables
customers
```
At this point, we can dump all the data from the table, but we won't necessarily know what each column means unless we look at the table information. First, let's use `PRAGMA table_info(customers);` to see the table information. Then we'll use `SELECT * FROM customers;` to dump the information from the table:

```
Linux
sqlite> PRAGMA table_info(customers);
0|cudtID|INT|1||1
1|custName|TEXT|1||0
2|creditCard|TEXT|0||0
3|password|TEXT|1||0

sqlite> SELECT * FROM customers;
0|Joy Paulson|4916 9012 2231 7905|5f4dcc3b5aa765d61d8327deb882cf99
1|John Walters|4671 5376 3366 8125|fef08f333cc53594c8097eba1f35726a
2|Lena Abdul|4353 4722 6349 6685|b55ab2470f160c331a99b8d8a1946b19
3|Andrew Miller|4059 8824 0198 5596|bc7b657bd56e4386e3397ca86e378f70
4|Keith Wayman|4972 1604 3381 8885|12e7a36c0710571b3d827992f4cfe679
5|Annett Scholz|5400 1617 6508 1166|e2795fc96af3f4d6288906a90a52a47f
```
We can see from the table information that there are four columns: `custID, custName, creditCard and password`. You may notice that this matches up with the results. Take the first row:

```
0|Joy Paulson|4916 9012 2231 7905|5f4dcc3b5aa765d61d8327deb882cf99
```
 
We have the custID (0), the custName (Joy Paulson), the creditCard (4916 9012 2231 7905) and a password hash (5f4dcc3b5aa765d61d8327deb882cf99).

In the next task, we'll look at cracking this hash.

We saw how to query an SQLite database for sensitive data in the previous task. We found a collection of password hashes, one for each user. In this task, we will briefly cover how to crack these.

When it comes to hash cracking, Kali comes pre-installed with various tools. If you know how to use these, then feel free to do so; however, they are outwith the scope of this material.

Instead, we will be using the online tool: Crackstation. This website is extremely good at cracking weak password hashes. For more complicated hashes, we would need more sophisticated tools; however, all of the crackable password hashes used in today's challenge are weak MD5 hashes, which Crackstation should handle very nicely.

When we navigate to the website, we are met with the following interface:
<img width="1011" height="318" alt="image" src="https://github.com/user-attachments/assets/413a685f-1e4d-4c41-9725-b442b7272858" />

Crackstation

Let's try pasting the password hash for Joy Paulson, which we found in the previous task (5f4dcc3b5aa765d61d8327deb882cf99). We solve the Captcha, then click the "Crack Hashes" button:

<img width="1012" height="395" alt="image" src="https://github.com/user-attachments/assets/30406a9d-760e-4bba-899c-62f7dab82491" />

Cracked Password

We see that the hash was successfully broken, and the user's password was "password". How secure!

It's worth noting that Crackstation works using a massive wordlist. If the password is not in the wordlist, then Crackstation will not be able to break the hash.

The challenge is guided, so if Crackstation fails to break a hash in today's box, you can assume that the hash has been specifically designed not to be crackable.

## 3. Injection

Injection flaws are very common in applications today. These flaws occur because the application interprets user-controlled input as commands or parameters. Injection attacks depend on what technologies are used and how these technologies interpret the input. 

#### Some common examples include:

* **SQL Injection:** This occurs when user-controlled input is passed to SQL queries. As a result, an attacker can pass in SQL queries to manipulate the outcome of such queries. This could potentially allow the attacker to access, modify and delete information in a database when this input is passed into database queries. This would mean an attacker could steal sensitive information such as personal details and credentials.
* **Command Injection:** This occurs when user input is passed to system commands. As a result, an attacker can execute arbitrary system commands on application servers, potentially allowing them to access users' systems.

#### The main defence for preventing injection attacks is ensuring that user-controlled input is not interpreted as queries or commands. There are different ways of doing this:

* **Using an allow list:** when input is sent to the server, this input is compared to a list of safe inputs or characters. If the input is marked as safe, then it is processed. Otherwise, it is rejected, and the application throws an error.
* **Stripping input:** If the input contains dangerous characters, these are removed before processing.
Dangerous characters or input is classified as any input that can change how the underlying data is processed. Instead of manually constructing allow lists or stripping input, various libraries exist that can perform these actions for you.

Dangerous characters or input is classified as any input that can change how the underlying data is processed. Instead of manually constructing allow lists or stripping input, various libraries exist that can perform these actions for you.

#### Command Injection

Command Injection occurs when server-side code (like PHP) in a web application makes a call to a function that interacts with the server's console directly. An injection web vulnerability allows an attacker to take advantage of that call to execute operating system commands arbitrarily on the server. The possibilities for the attacker from here are endless: they could list files, read their contents, run some basic commands to do some recon on the server or whatever they wanted, just as if they were sitting in front of the server and issuing commands directly into the command line. 

Once the attacker has a foothold on the web server, they can start the usual enumeration of your systems and look for ways to pivot around.

#### Code Example

Let's consider a scenario: MooCorp has started developing a web-based application for cow ASCII art with customisable text. While searching for ways to implement their app, they've come across the cowsay command in Linux, which does just that! Instead of coding a whole web application and the logic required to make cows talk in ASCII, they decide to write some simple code that calls the cowsay command from the operating system's console and sends back its contents to the website.

Let's look at the code they used for their app.  See if you can determine why their implementation is vulnerable to command injection.  We'll go over it below.

<img width="572" height="266" alt="Screenshot 2025-08-13 at 21 58 22" src="https://github.com/user-attachments/assets/71986e90-5aa4-49cd-8a76-ecdcad0814ec" />

In simple terms, the above snippet does the following:

Checking if the parameter `"mooing"` is set. If it is, the variable $mooing gets what was passed into the input field.
Checking if the parameter `"cow"` is set. If it is, the variable $cow gets what was passed through the parameter.
The program then executes the function `passthru("perl /usr/bin/cowsay -f $cow $mooing");`. The passthru function simply executes a command in the operating system's console and sends the output back to the user's browser. You can see that our command is formed by concatenating the $cow and $mooing variables at the end of it. Since we can manipulate those variables, we can try injecting additional commands by using simple tricks. If you want to, you can read the docs on `passthru()` on PHP's website for more information on the function itself.

<img width="1438" height="420" alt="image" src="https://github.com/user-attachments/assets/51ea3879-cd64-4fec-a1c9-d063a5d120ed" />

#### Exploiting Command Injection

Now that we know how the application works behind the curtains, we will take advantage of a bash feature called "inline commands" to abuse the cowsay server and execute any arbitrary command we want. Bash allows you to run commands within commands. This is useful for many reasons, but in our case, it will be used to inject a command within the cowsay server to get it executed.

To execute inline commands, you only need to enclose them in the following format `$(your_command_here)`. If the console detects an inline command, it will execute it first and then use the result as the parameter for the outer command. Look at the following example, which runs `whoami` as an inline command inside an `echo` command:

<img width="1572" height="392" alt="image" src="https://github.com/user-attachments/assets/cc67f9cb-86e4-4c90-851d-b68ae9867bde" />

So coming back to the cowsay server, here's what would happen if we send an inline command to the web application:

<img width="1501" height="482" alt="image" src="https://github.com/user-attachments/assets/40682ee5-dfa5-4684-a2cb-0aba201eb065" />

Since the application accepts any input from us, we can inject an inline command which will get executed and used as a parameter for cowsay. This will make our cow say whatever the command returns! In case you are not that familiar with Linux, here are some other commands you may want to try:

- whoami
- id
- ifconfig/ip addr
- uname -a
- ps -ef

## 4. Insecure Design

**Insecure design** refers to **vulnerabilities which are inherent to the application's architecture**. They are not vulnerabilities regarding bad implementations or configurations, but the idea behind the whole application (or a part of it) is flawed from the start. Most of the time, **these vulnerabilities occur when an improper threat modelling is made during the planning phases of the application and propagate all the way up to your final app**. Some other times, **insecure design vulnerabilities may also be introduced by developers while adding some "shortcuts" around the code to make their testing easier**. A developer could, for example, **disable the OTP validation in the development phases to quickly test the rest of the app without manually inputting a code at each login but forget to re-enable it when sending the application to production**.

### Insecure Password Resets

A good example of such **vulnerabilities occurred on Instagram a while ago**. Instagram allowed users to reset their forgotten passwords by sending them a 6-digit code to their mobile number via SMS for validation. If an attacker wanted to access a victim's account, he could try to brute-force the 6-digit code. As expected, this was not directly possible as Instagram had rate-limiting implemented so that after 250 attempts, the user would be blocked from trying further.

<img width="1413" height="390" alt="image" src="https://github.com/user-attachments/assets/a390bb4c-cf91-4777-b9b5-eff95fe49311" />

However, it was found that the rate-limiting only applied to code attempts made from the same IP. If an attacker had several different IP addresses from where to send requests, he could now try 250 codes per IP. For a 6-digit code, you have a million possible codes, so an attacker would need 1000000/250 = 4000 IPs to cover all possible codes. This may sound like an insane amount of IPs to have, but cloud services make it easy to get them at a relatively small cost, making this attack feasible.

<img width="1311" height="659" alt="image" src="https://github.com/user-attachments/assets/04e6f0cf-1bd5-40fe-88ff-73cee642ba89" />

Notice how the vulnerability is related to the idea that no user would be capable of using thousands of IP addresses to make concurrent requests to try and brute-force a numeric code. The problem is in the design rather than the implementation of the application in itself.

## 5. Security Misconfiguration

**Security Misconfigurations** are distinct from the other Top 10 vulnerabilities because they occur when security could have been appropriately configured but was not. Even if you download the latest up-to-date software, poor configurations could make your installation vulnerable.

Security misconfigurations include:

Poorly configured permissions on cloud services, like S3 buckets.
Having unnecessary features enabled, like services, pages, accounts or privileges.
Default accounts with unchanged passwords.
Error messages that are overly detailed and allow attackers to find out more about the system.
Not using HTTP security headers.
This vulnerability can often lead to more vulnerabilities, such as default credentials giving you access to sensitive data, XML External Entities (XXE) or command injection on admin pages.

For more info, look at the OWASP top 10 entry for Security Misconfiguration.

### Debugging Interfaces

A common security misconfiguration concerns the exposure of debugging features in production software. Debugging features are often available in programming frameworks to allow the developers to access advanced functionality that is useful for debugging an application while it's being developed. Attackers could abuse some of those debug functionalities if somehow, the developers forgot to disable them before publishing their applications.

One example of such a vulnerability was allegedly used when Patreon got hacked in 2015. Five days before Patreon was hacked, a security researcher reported to Patreon that he had found an open debug interface for a Werkzeug console. Werkzeug is a vital component in Python-based web applications as it provides an interface for web servers to execute the Python code. Werkzeug includes a debug console that can be accessed either via URL on /console, or it will also be presented to the user if an exception is raised by the application. In both cases, the console provides a Python console that will run any code you send to it. For an attacker, this means he can execute commands arbitrarily.

<img width="655" height="327" alt="image" src="https://github.com/user-attachments/assets/e1509654-f90d-4bd9-94ef-30e67a6a5dc9" />

## 6. Vulnerable and Outdated Components

Occasionally, you may find that the company/entity you're pen-testing is using a program with a well-known vulnerability.

For example, let's say that a company hasn't updated their version of WordPress for a few years, and using a tool such as WPScan, you find that it's version 4.6. Some quick research will reveal that WordPress 4.6 is vulnerable to an unauthenticated remote code execution(RCE) exploit, and even better, you can find an exploit already made on Exploit-DB.

As you can see, this would be quite devastating because it requires very little work on the attacker's part. Since the vulnerability is already well known, someone else has likely made an exploit for the vulnerability already. The situation worsens when you realise that it's really easy for this to happen. If a company misses a single update for a program they use, it could be vulnerable to any number of attacks.

### Vulnerable and Outdated Components - Exploit

Recall that since this is about known vulnerabilities, most of the work has already been done for us. Our main job is to find out the information of the software and research it until we can find an exploit. Let's go through that with an example web application.

<img width="476" height="327" alt="image" src="https://github.com/user-attachments/assets/c7faef64-d06e-416d-97ac-aa309708a673" />

What do you know? This server has the default page for the Nostromo web server. Now that we have a version number and a software name, we can use Exploit-DB to try and find an exploit for this particular version.

<img width="849" height="265" alt="image" src="https://github.com/user-attachments/assets/07c756f2-556e-47ed-b356-362641fe4201" />

Lucky us, the top result happens to be an exploit script. Let's download it and try to get code execution. Running this script on its own teaches us a very important lesson.

```
user@linux$ python 47837.py
Traceback (most recent call last):
  File "47837.py", line 10, in <module>
    cve2019_16278.py
NameError: name 'cve2019_16278' is not defined
```
Exploits you download from the Internet may not work the first time. It helps to understand the programming language the script is in so that, if needed, you can fix any bugs or make any modifications, as quite a few scripts on Exploit-DB expect you to make modifications.

Fortunately, the error was caused by a line that should have been commented out, so it's an easy fix.

```
# Exploit Title: nostromo 1.9.6 - Remote Code Execution
# Date: 2019-12-31
# Exploit Author: Kr0ff
# Vendor Homepage:
# Software Link: http://www.nazgul.ch/dev/nostromo-1.9.6.tar.gz
# Version: 1.9.6
# Tested on: Debian
# CVE : CVE-2019-16278

cve2019_16278.py  # This line needs to be commented.

#!/usr/bin/env python

```

Fixing that, let's try and run the program again.

```
user@linux$ python2 47837.py 127.0.0.1 80 id

                                        _____-2019-16278
        _____  _______    ______   _____\    \
   _____\    \_\      |  |      | /    / |    |
  /     /|     ||     /  /     /|/    /  /___/|
 /     / /____/||\    \  \    |/|    |__ |___|/
|     | |____|/ \ \    \ |    | |       \
|     |  _____   \|     \|    | |     __/ __
|\     \|\    \   |\         /| |\    \  /  \
| \_____\|    |   | \_______/ | | \____\/    |
| |     /____/|    \ |     | /  | |    |____/|
 \|_____|    ||     \|_____|/    \|____|   | |
        |____|/                        |___|/

HTTP/1.1 200 OK
Date: Fri, 03 Feb 2023 04:58:34 GMT
Server: nostromo 1.9.6
Connection: close

uid=1001(_nostromo) gid=1001(_nostromo) groups=1001(_nostromo)
```
Boom! We have RCE. Now it's important to note that most scripts will tell you what arguments you need to provide. Exploit developers will rarely make you read potentially hundreds of lines of code just to figure out how to use the script.

It is also worth noting that it may not always be this easy. Sometimes you will just be given a version number, like in this case, but other times you may need to dig through the HTML source or even take a lucky guess on an exploit script. But realistically, if it is a known vulnerability, there's probably a way to discover what version the application is running.

That's really it. The great thing about this piece of the OWASP Top 10 is that the work is already done for us, we just need to do some basic research, and as a penetration tester, you're already doing that quite a bit.

## 7. Identification and Authentication Failures

Authentication and session management constitute core components of modern web applications. Authentication allows users to gain access to web applications by verifying their identities. The most common form of authentication is using a username and password mechanism. A user would enter these credentials, and the server would verify them. The server would then provide the users' browser with a session cookie if they are correct. A session cookie is needed because web servers use HTTP(S) to communicate, which is stateless. Attaching session cookies means the server will know who is sending what data. The server can then keep track of users' actions. 

<img width="1742" height="482" alt="image" src="https://github.com/user-attachments/assets/17824952-a56c-4f2f-85f1-28b15d4d5095" />

If an attacker is able to find flaws in an authentication mechanism, they might successfully gain access to other users' accounts. This would allow the attacker to access sensitive data (depending on the purpose of the application). Some common flaws in authentication mechanisms include the following:

- **Brute force attacks**: If a web application uses usernames and passwords, an attacker can try to launch brute force attacks that allow them to guess the username and passwords using multiple authentication attempts. 
- **Use of weak credentials**: Web applications should set strong password policies. If applications allow users to set passwords such as "password1" or common passwords, an attacker can easily guess them and access user accounts.
- **Weak Session Cookies**: Session cookies are how the server keeps track of users. If session cookies contain predictable values, attackers can set their own session cookies and access users' accounts. 

There can be various mitigation for broken authentication mechanisms depending on the exact flaw:

To avoid password-guessing attacks, ensure the application enforces a strong password policy. 
To avoid brute force attacks, ensure that the application enforces an automatic lockout after a certain number of attempts. This would prevent an attacker from launching more brute-force attacks.

Implement Multi-Factor Authentication. If a user has multiple authentication methods, for example, using a username and password and receiving a code on their mobile device, it would be difficult for an attacker to get both the password and the code to access the account.

For this example, we'll look at a logic flaw within the authentication mechanism.

Many times, what happens is that developers forget to sanitise the input(username & password) given by the user in the code of their application, which can make them vulnerable to attacks like SQL injection. However, we will focus on a vulnerability that happens because of a developer's mistake but is very easy to exploit, i.e. re-registration of an existing user.

Let's understand this with the help of an example, say there is an existing user with the name admin, and we want access to their account, so what we can do is try to re-register that username but with slight modification. We will enter `admin` without the quotes (notice the space at the start). Now when you enter that in the username field and enter other required information like email id or password and submit that data, it will register a new user, but that user will have the same right as the admin account. That new user will also be able to see all the content presented under the user `admin`.

To see this in action, go to http://MACHINE_IP:8088 and try to register with `darren` as your username. You'll see that the user already exists, so try to register `darren` instead, and you'll see that you are now logged in and can see the content present only in darren's account, which in our case, is the flag that you need to retrieve.


