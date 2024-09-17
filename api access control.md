### **API Access Control and Authorization in Detail**

**API Access Control and Authorization** are critical to ensuring that only authorized users or systems can interact with APIs, protecting resources and services from unauthorized access or misuse. These mechanisms are essential to API security and play a vital role in managing who can access the API and how they can use it.



---

### **API Access Control Methods**

1. **API Key-Based Access Control**:
   - Involves assigning a unique key to each API consumer. Consumers include this key in their requests to authenticate.
   - It is simple but less secure than token-based approaches like OAuth2 or JWT.

   Example:
   - API request with an API key:
     ```bash
     curl -X GET https://api.example.com/v1/resources \
     -H "Authorization: API-Key abc123xyz"
     ```

2. **OAuth 2.0**:
   - OAuth 2.0 is a widely used framework for delegated authorization. The API consumer (client) obtains an **access token** from an **authorization server** after successful authentication.
   - The token is then included in API requests to authenticate and authorize the client.

   OAuth 2.0 consists of four grant types:
   - **Authorization Code**: Used by web and mobile apps where the client exchanges an authorization code for an access token.
   - **Client Credentials**: Used when the client is a trusted application that directly interacts with the API.
   - **Password Grant**: Used when the user provides credentials directly to the API consumer.
   - **Implicit Grant**: Used by single-page applications (not recommended due to security concerns).

3. **JWT (JSON Web Tokens)**:
   - JWTs are used to pass user claims between systems in a compact and secure format. They are digitally signed and can be verified by the API to grant access.
   - JWT tokens contain three parts: **Header**, **Payload**, and **Signature**.
   - The payload often includes claims like user roles, expiration time, and permissions (scopes).
   
   Example JWT structure:
   ```json
   {
     "alg": "HS256", 
     "typ": "JWT"
   }{
     "sub": "user@example.com", 
     "roles": ["admin"], 
     "exp": 1620000000
   }{
     "signature"
   }
   ```

   - JWT is passed in the Authorization header:
     ```bash
     curl -X GET https://api.example.com/v1/orders \
     -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR..."
     ```

4. **Role-Based Access Control (RBAC)**:
   - RBAC restricts access to APIs based on the roles assigned to users. It defines a set of roles and associates them with permissions.
   - Users or applications with specific roles (e.g., `admin`, `editor`, `viewer`) can only perform actions they are authorized for.

5. **OAuth Scopes**:
   - OAuth scopes limit what an API client can do with the access granted by a token. Scopes define the API's available actions (e.g., `read`, `write`, `admin`).
   - When requesting an OAuth token, clients can specify the scopes they require.

---

### **Working Example: OAuth2 in WSO2 API Manager**

#### **Step 1: Set up OAuth2 Authorization for an API in WSO2 API Manager**

1. **Create a New API**:
   - Log into the **WSO2 API Publisher** portal.
   - Click **Create API** and choose either to design a new API or import an existing OpenAPI definition.
   - Define API details such as the name, version, context (URL path), and resources.

2. **Enable OAuth2 for the API**:
   - Under the **API Details**, navigate to **Manage** → **Security**.
   - Enable **OAuth2** as the authorization method for the API.
   - Optionally configure throttling tiers to define usage limits.

3. **Publish the API**:
   - After configuring the OAuth2 settings, click **Save & Publish** to make the API available for subscription in the Developer Portal.

#### **Step 2: Subscribe to the API**

1. **Go to the Developer Portal**:
   - Log into the **WSO2 API Developer Portal**.
   - Find the published API and click on it to view the API details.

2. **Subscribe to the API**:
   - Click **Subscribe**, choose a **subscription tier** (which defines access limits), and generate an **OAuth2 client** (application).
   - This generates **Client ID** and **Client Secret**, which will be used to obtain an OAuth2 token.

#### **Step 3: Obtain an OAuth2 Token**

1. **Send a Token Request**:
   - To consume the API, you must first request an OAuth2 token from the token endpoint.
   
   Example `cURL` command to request a token using the **client credentials grant**:
   ```bash
   curl -k -d "grant_type=client_credentials" \
   -H "Authorization: Basic <Base64(client_id:client_secret)>" \
   -H "Content-Type: application/x-www-form-urlencoded" \
   https://<WSO2-API-Manager>/oauth2/token
   ```

   - Replace `<Base64(client_id:client_secret)>` with the base64-encoded client ID and client secret obtained during subscription.

2. **Response**:
   - The server responds with an access token in JSON format:
     ```json
     {
       "access_token": "eyJhbGciOiJSUzI1NiIsInR...",
       "token_type": "Bearer",
       "expires_in": 3600
     }
     ```

#### **Step 4: Make Authorized API Requests**

1. **Call the API**:
   - After obtaining the access token, you can make authorized API requests by including the token in the **Authorization** header.

   Example:
   ```bash
   curl -X GET https://<WSO2-API-Manager>/api/v1/resource \
   -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR..."
   ```

2. **Handle Responses**:
   - The API responds with the requested data if the token is valid and the user has the required permissions.

