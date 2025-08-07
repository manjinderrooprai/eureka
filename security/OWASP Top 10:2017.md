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

