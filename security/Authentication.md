# Authentication

### **What is Authentication?**

Authentication is the process of **verifying a user's identity** to confirm who they are and whether they have permission to access a system. It is the first step in the security process, acting as a gatekeeper. When a user sends a login request, the authentication process checks their credentials and either grants or denies them access.

<img width="987" height="385" alt="Screenshot 2025-08-14 at 09 51 31" src="https://github.com/user-attachments/assets/8587b614-7c15-49ba-b1b8-f209136029d4" />

* It's important to distinguish authentication from **authorization**. While authentication confirms **who you are**, authorization determines **what you are allowed to do** after you have been authenticated.

<img width="987" height="485" alt="Screenshot 2025-08-14 at 09 52 41" src="https://github.com/user-attachments/assets/1cc9d708-16ce-42b3-83b4-da46126c1318" />

## **Types of Authentication**

- **1. Basic Authentication**
- **2. Bearer Tokens**
- **3. OAuth 2.0 and JWT Tokens**
- **4. Access and Refresh Tokens**
- **5. Single Sign-On (SSO) and Identity Protocols**

### **1. Basic Authentication**

This is a simple method where a **username and password** are sent with a request. These credentials are combined and encoded using Base64.

* **Weakness**: The main issue with this method is that Base64 encoding is easily reversible, meaning the username and password can be exposed if not sent over a secure HTTPS connection.
* **Modern Usage**: Due to its security risks, it is rarely used today, except for some internal company tools.
* **Tools & Technologies:**
    * **Web Servers:** It can be configured directly in web servers like **Apache** (using `.htpasswd` files) or **Nginx**.
    * **API Clients:** Tools like **Postman**, **Insomnia**, or the command-line tool **`curl`** are used to send requests with Basic Authentication headers for testing.

<img width="1086" height="741" alt="Screenshot 2025-08-14 at 09 58 07" src="https://github.com/user-attachments/assets/2ab5e96b-9509-491d-a9d0-1d8a9d99f16d" />

### **2. Bearer Tokens**

A more secure and common approach, especially for APIs. Instead of credentials, a **bearer token** (an access token) is sent with each request to access resources.

* **How it Works**: The API receives the request, verifies the token, and if valid, sends back the requested data.
* **Advantages**: This method is fast, scalable, and **stateless**, meaning the server doesn't need to store session information between requests, making it the current standard for API design.
* **Tools & Technologies:**
    * **API Gateways:** Services like **Amazon API Gateway**, **Kong**, and **Tyk** manage and secure APIs using bearer tokens.
    * **Web Frameworks:** Backend frameworks use libraries to handle token validation. Examples include **Passport.js** (for Node.js/Express), **Spring Security** (for Java), and **Django REST Framework** (for Python).

<img width="984" height="593" alt="Screenshot 2025-08-14 at 09 59 31" src="https://github.com/user-attachments/assets/0464774b-4baf-4bbb-9eac-ad93a25eaad0" />

### **3. OAuth 2.0 and JWT Tokens**

**OAuth 2.0** is an authorization protocol that allows users to log in through trusted third-party providers like Google or GitHub.

* **How it Works**: When a user authenticates via a provider like Google, that service sends a **JSON Web Token (JWT)** to the application.
* **JWT Details**: This token is a signed object containing user information like user ID, email, and an expiration date. The application then passes this JWT to the API to authenticate the user. Like bearer tokens, JWTs are stateless.
* **Tools & Technologies:**
    * **OAuth Providers:** You see this every day with "Log in with..." buttons. Major providers include **Google**, **Facebook**, **GitHub**, and enterprise solutions like **Okta** and **Auth0**.
    * **JWT Libraries:** Developers use libraries to create and verify JWTs. Popular examples are **`jsonwebtoken`** for Node.js, **`PyJWT`** for Python, and **`nimbus-jose-jwt`** for Java.

<img width="1310" height="732" alt="Screenshot 2025-08-14 at 10 00 30" src="https://github.com/user-attachments/assets/7b88aab5-afda-4cf1-a9d4-1c9aa88ddd21" />

### **4. Access and Refresh Tokens**

Modern systems enhance security by using two types of tokens:

* **Access Tokens**: These are **short-lived** tokens used for making API calls to access data. Their short lifespan minimizes risk if the token is compromised.
* **Refresh Tokens**: These are **long-lived** tokens whose sole purpose is to get a new access token when the current one expires. This allows users to remain logged in without interruption. For security, refresh tokens are typically stored on the server side.
* **Tools & Technologies:**
    * **Identity Platforms:** Services like **Auth0**, **Okta**, **Firebase Authentication**, and **Microsoft Entra ID** manage the entire access and refresh token lifecycle out of the box.
    * **Client-Side Libraries:** HTTP clients like **Axios** can be configured with "interceptors" to automatically use the refresh token to get a new access token when a request fails, providing a seamless user experience.

<img width="1358" height="774" alt="Screenshot 2025-08-14 at 10 01 20" src="https://github.com/user-attachments/assets/ba894a97-aac3-491d-9d48-f848e8d0ced0" />

### **5. Single Sign-On (SSO) and Identity Protocols**

**Single Sign-On (SSO)** allows users to log in once and gain access to multiple related services without needing to re-authenticate for each one.

* **Identity Protocols**: These are the frameworks that allow SSO to work by securely exchanging user login information between different applications. Folloeing two main protocols:
    * **SAML (Security Assertion Markup Language)**: An older, XML-based protocol still common in enterprise environments.
    * **OAuth 2.0**: The more modern, JSON-based protocol that is widely used today.
* **Tools & Technologies:**
    * **SAML (Security Assertion Markup Language):** An older, XML-based protocol still widely used in corporate environments.
        * **Providers:** **Microsoft ADFS (Active Directory Federation Services)**, **Shibboleth**, **Okta**, and **Ping Identity**.
    * **OpenID Connect (OIDC):** A modern identity layer built on top of OAuth 2.0. It's what enables most "social login" scenarios.
        * **Providers:** **Google**, **Microsoft Entra ID**, and open-source solutions like **Keycloak**.
<img width="1293" height="748" alt="Screenshot 2025-08-14 at 10 01 54" src="https://github.com/user-attachments/assets/871ad9e0-1ebe-46c6-a035-8ce0362d0d09" />
