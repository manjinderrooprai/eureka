## **How OpenID Connect (OIDC) Works**
OpenID Connect (OIDC) is an authentication protocol built on top of **OAuth 2.0**. It allows clients (such as web apps or mobile apps) to verify a user's identity based on authentication performed by an **Identity Provider (IdP)**.

OIDC enables **single sign-on (SSO)** and provides a way to obtain identity information about the user in a secure and standardized manner.

## **OIDC vs. OAuth 2.0**
- **OAuth 2.0**: Used for **authorization** (grants access to resources).
- **OIDC**: Used for **authentication** (verifies user identity).

OIDC extends OAuth 2.0 by introducing the **ID Token**, which contains information about the authenticated user.

## **OIDC Flow (Authorization Code Flow)**
### **1. User Requests Authentication**
- The user visits a web or mobile application and chooses to log in using an **OIDC Identity Provider (IdP)** like Apple, Google, or Okta.
- The client (your app) **redirects the user** to the IdP's authorization endpoint.

**Example URL to redirect the user:**
```
https://appleid.apple.com/auth/authorize
  ?client_id=YOUR_CLIENT_ID
  &redirect_uri=https://your-app.com/callback
  &response_type=code
  &scope=openid email profile
  &state=RANDOM_STRING
```

### **2. User Authenticates with the IdP**
- The user logs in at the **Identity Provider (IdP)** (e.g., Apple, Google).
- If authentication is successful, the IdP generates an **authorization code**.
- The IdP redirects the user back to your app's **redirect URI**, sending the **authorization code**.

Example callback:
```
https://your-app.com/callback?code=AUTH_CODE&state=RANDOM_STRING
```

### **3. App Exchanges Code for Tokens**
The application sends a **POST request** to the **IdP’s Token Endpoint** to exchange the **authorization code** for **tokens**.

**Example Request:**
```http
POST https://appleid.apple.com/auth/token
Content-Type: application/x-www-form-urlencoded

client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET
&code=AUTH_CODE
&grant_type=authorization_code
&redirect_uri=https://your-app.com/callback
```

#### **Response:**
The IdP responds with:
```json
{
  "id_token": "eyJhbGciOi...",
  "access_token": "xyz123",
  "refresh_token": "abcd456",
  "expires_in": 3600
}
```

### **4. App Validates the ID Token**
- The **ID Token** is a **JWT (JSON Web Token)** containing user identity details.
- The app **validates the ID token** using the IdP’s public key.
- The app **extracts user details** (e.g., email, name) from the **ID token payload**.

#### **Decoded ID Token Example:**
```json
{
  "sub": "1234567890",
  "email": "user@example.com",
  "name": "John Doe",
  "iat": 1710000000,
  "exp": 1710003600,
  "aud": "YOUR_CLIENT_ID",
  "iss": "https://appleid.apple.com"
}
```

✅ **Validation Checklist:**
- Ensure `iss` (issuer) matches the IdP (`https://appleid.apple.com`).
- Ensure `aud` (audience) matches your client ID.
- Ensure `exp` (expiration) is valid.

### **5. User is Authenticated**
- The app now recognizes the user as **authenticated**.
- The app can create a **session** or issue an **application token** to keep the user logged in.
- The app can now make **authorized requests** using the `access_token`.

### **6. Access Protected Resources (Optional)**
If the app needs to access **protected user data** (e.g., calendar, photos), it can use the **access token**.

Example API request using the access token:
```http
GET https://api.example.com/userinfo
Authorization: Bearer xyz123
```

### **7. Refresh Token (Optional)**
If the user session expires, the app can use the **refresh token** to get a new **access token** without requiring the user to log in again.

**Example Refresh Request:**
```http
POST https://appleid.apple.com/auth/token
Content-Type: application/x-www-form-urlencoded

client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET
&grant_type=refresh_token
&refresh_token=abcd456
```

## **Summary of OIDC Components**
| **Component**  | **Purpose** |
|---------------|------------|
| **Authorization Code** | Temporary code used to exchange for tokens. |
| **ID Token** | JWT containing user identity details. |
| **Access Token** | Token for accessing protected resources. |
| **Refresh Token** | Used to get a new access token without re-authentication. |
| **UserInfo Endpoint** | API that provides user profile details. |

## **OIDC Authentication Flow Diagram**
```
1. User clicks "Login with Apple"
2. App redirects to Apple OIDC
3. User logs in with Apple ID
4. Apple redirects back with authorization code
5. App exchanges code for ID token & access token
6. App validates ID token and extracts user info
7. User is authenticated and logged in
```

## **Best Practices**
✅ **Always Validate the ID Token**  
✅ **Use HTTPS for Secure Communication**  
✅ **Rotate Client Secrets Regularly**  
✅ **Use Short-Lived Access Tokens & Refresh Tokens**  
✅ **Restrict Scopes to Only Necessary Information**  

## **Conclusion**
OIDC is a secure and standardized way to authenticate users while leveraging OAuth 2.0. It ensures strong authentication, user identity verification, and SSO capabilities across different applications.
