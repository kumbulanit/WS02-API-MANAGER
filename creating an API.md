### Creating, Publishing, and Managing APIs in WSO2 API Manager

WSO2 API Manager (APIM) offers a comprehensive platform to create, publish, manage, and secure APIs. The process typically involves multiple stages, from API creation to publishing and managing its lifecycle. Below is a step-by-step guide for each of these processes:

---

### 1. **Creating an API**
   
   **Steps:**
   1. **Login to WSO2 API Publisher**:
      - Access the API Publisher Portal via the URL: `https://<hostname>:9443/publisher`
      - Login with the appropriate credentials (default is `admin/admin`).

   2. **Create a New API**:
      - On the API Publisher dashboard, click **Create API**.
      - Choose between several methods of API creation:
         - **Design a New REST API**: Create an API from scratch by defining its resources.
         - **Import OpenAPI Specification**: Upload an OpenAPI (Swagger) definition to automatically create the API.
         - **SOAP or WebSocket API**: Create SOAP or WebSocket APIs.
         - **Service Catalog**: Import a service from the service catalog (this is for microservices discovery).

   3. **Basic Information**:
      - Provide the API’s **Name**, **Context Path** (base URL), **Version**, and **Business Plan**.
      - Define **Endpoint URLs** for the production and sandbox environments.

   4. **Define Resources**:
      - Resources (API methods/endpoints) can be added manually if creating the API from scratch. This includes HTTP methods like `GET`, `POST`, `PUT`, `DELETE`.
      - Set authentication and throttling levels for each resource.

   5. **Additional Configurations**:
      - **Security**: Enable OAuth2, API Key, or JWT token authentication.
      - **Throttling**: Set rate-limiting policies.
      - **CORS**: Define Cross-Origin Resource Sharing (CORS) rules.

---

### 2. **Publishing the API**

   After defining the API, the next step is publishing it so developers can discover and use it.

   **Steps:**
   1. **Lifecycle Management**:
      - In the API Publisher, navigate to the **Lifecycle** tab of your API.
      - Change the API state from **Created** to **Published**.
      - Optionally, configure a workflow for approvals before the API is made public.

   2. **Subscriptions and Access**:
      - Define whether the API should be publicly accessible or if developers need to subscribe to access it.
      - Create and attach subscription tiers (throttling policies) to the API.
      - Optionally, allow sandbox testing for APIs to be used in a lower environment before full production release.

   3. **API Gateway Deployment**:
      - Once published, the API is deployed to the API Gateway.
      - The Gateway handles traffic routing, security enforcement, and rate-limiting.

   4. **Expose via Developer Portal**:
      - Published APIs become available on the **WSO2 Developer Portal** (`https://<hostname>:9443/devportal`).
      - Developers can explore the API catalog, register, subscribe to APIs, and get access tokens.

---

