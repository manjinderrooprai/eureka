# API Security: 7 Techniques to Protect Your APIs

<img width="870" height="593" alt="API Security" src="https://github.com/user-attachments/assets/88a9cbeb-5da2-4248-8098-31eec26b3efd" style="border: 5px solid #333; border-radius: 15px;" />

### 1. Rate Limiting

* **Definition:** A security measure that restricts the number of requests a client can make to an API within a defined period.
* **Explanation:** This acts as a gatekeeper, preventing any single user or client from sending an excessive number of requests to ensure the API remains available and responsive for everyone.
* **Cause:** The primary cause it addresses is potential abuse, such as a Denial-of-Service (DoS) or a Distributed Denial-of-Service (DDoS) attack, where a system is flooded with requests to make it unavailable.
* **Solution Examples:**
    * **Per-User Limit:** Setting a limit of 100 requests per user for a specific period. If the user exceeds this, their subsequent requests are temporarily blocked.
    * **Per-Endpoint Limit:** Applying a more restrictive limit on a particular endpoint, like `/comments`, to prevent a single user from spamming.
    * **Global Rate Limit:** Implementing an overall limit across the entire API to protect against large-scale DDoS attacks.

<img width="857" height="575" alt="Rate Limiting" src="https://github.com/user-attachments/assets/dbf68143-bcb1-4414-a38b-7d607eea2f11" />

### 2. Cross-Origin Resource Sharing (CORS)

* **Definition:** A security feature that controls which domains are allowed to access your API from a web browser.
* **Explanation:** When a browser makes a request from a different domain than the API, CORS determines if that request should be permitted. It uses special HTTP headers to manage this communication.
* **Cause:** The security threat it mitigates is a malicious website attempting to trick a user's browser into making unauthorized requests to your API while the user is logged in.
* **Solution Examples:**
    * **Whitelist Specific Domains:** Configuring the API to only accept requests from a trusted domain, such as your own frontend application (`app.yourdomain.com`).
    * **Open Access:** For public APIs, a less restrictive policy might be used that allows requests from any domain, often signified by a wildcard (`*`).

<img width="837" height="544" alt="Cross-Origin Resource Sharing (CORS)" src="https://github.com/user-attachments/assets/8a490c9e-57dc-4d4a-b8d4-4cb71e23500f" />

### 3. SQL and NoSQL Injections

* **Definition:** An attack where malicious user input is used to manipulate the logic of a database query.
* **Explanation:** Instead of providing expected data, the attacker provides code that, when executed, can alter the database query. This can lead to unauthorized data access, modification, or deletion.
* **Cause:** This vulnerability is caused by a lack of proper sanitization and validation of user input before it's used in a database query.
* **Solution Examples:**
    * **Parameterized Queries:** Using prepared statements where the query structure is defined first, and the user-provided data is added separately, preventing the input from being executed as code.
    * **Object-Relational Mapper (ORM):** Utilizing an ORM library, which automatically handles the sanitization and secure execution of database queries.

<img width="941" height="440" alt="SQL and NoSQL Injections" src="https://github.com/user-attachments/assets/9f223f6e-555a-473f-8dd2-bf1438dbcd36" />

### 4. Firewall

* **Definition:** A firewall acts as a gatekeeper between your API and incoming traffic, filtering out malicious requests.
* **Explanation:** It is a security system that monitors and controls incoming and outgoing network traffic based on predefined security rules.
* **Cause:** It addresses various threats by inspecting traffic for suspicious patterns, preventing known attack vectors from reaching the API.
* **Solution and Examples:**
    * A **Web Application Firewall (WAF)**, like the one provided by AWS, can block requests that have unusual HTTP methods or known SQL injection keywords, allowing only legitimate traffic to pass through.

<img width="928" height="554" alt="Firewall" src="https://github.com/user-attachments/assets/419871f2-d999-4114-8dd8-a0a76fa447d1" />

### 5. Virtual Private Network (VPN)

* **Definition:** A VPN is a technology that restricts API access to a specific, private network, ensuring that only authorized clients can connect.
* **Explanation:** It creates a secure tunnel for network traffic, hiding your IP address and encrypting your data. When used for an API, it ensures that only devices within the VPN can communicate with it.
* **Cause:** It addresses the need to protect sensitive, internal APIs from any access from the public internet.
* **Solution and Examples:**
    * If you have an internal admin dashboard with an API that should only be accessible by employees, you can place this API within a **company VPN**. Only employees connected to the VPN would be able to access the API, while all external users would be blocked.

<img width="966" height="543" alt="Virtual Private Network (VPN)" src="https://github.com/user-attachments/assets/45a492fe-8b69-4107-bdee-082b1f98c617" />

### 6. Cross-Site Request Forgery (CSRF)

* **Definition:** An attack where a malicious website or attacker tricks a user's browser into making an unwanted request to an API on their behalf.
* **Explanation:** This attack leverages the fact that a user's browser automatically sends session cookies with requests. If the user is logged into a vulnerable site, an attacker can trick their browser into performing an action without their knowledge.
* **Cause:** This vulnerability arises when an API trusts that a request is legitimate simply because it has a valid session cookie.
* **Solution Examples:**
    * **CSRF Tokens:** A common solution is to include a unique, secret token in every form or request. The API then verifies this token, and if it doesn't match, the request is blocked.
    * **Double Submit Cookie:** A method where a CSRF token is stored in both a cookie and a hidden field in the form. The server validates that both values match.
  
<img width="723" height="543" alt="Cross-Site Request Forgery (CSRF)" src="https://github.com/user-attachments/assets/7f572a4c-75eb-4269-83b9-55451c17da87" />

### 7. Cross-Site Scripting (XSS)

* **Definition:** A security vulnerability that allows an attacker to inject malicious scripts into a web page that is then viewed by other users.
* **Explanation:** The injected script is then executed by the victim's browser, enabling the attacker to steal sensitive information, impersonate the user, or perform other malicious actions.
* **Cause:** This vulnerability is a result of a web application not properly validating, sanitizing, or encoding user-provided data before displaying it to other users.
* **Solution Examples:**
    * **Input Sanitization:** Filtering or removing any potentially malicious characters or tags from user input before saving it to the database.
    * **Output Encoding:** Escaping special characters in the data when it is rendered on the web page, so the browser interprets the input as text rather than executable code.

<img width="1117" height="543" alt="Cross-Site Scripting (XSS)" src="https://github.com/user-attachments/assets/ce029c3c-2207-4fe2-bbee-41bacb66be5e" />

