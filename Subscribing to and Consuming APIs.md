### Subscribing to and Consuming APIs in WSO2 API Manager

Once an API is created and published, developers can subscribe to it through the **WSO2 Developer Portal**. API consumers can then use the subscribed APIs to build applications or services. The subscription process ensures that only authorized users can access the API, and it helps manage and monitor usage.

Here’s a step-by-step guide on subscribing to and consuming APIs in WSO2 API Manager:

---

### 1. **Subscribing to APIs**

#### a. **Access the Developer Portal**
- Navigate to the **WSO2 Developer Portal** via the URL:  
  `https://<hostname>:9443/devportal`.
- Log in using your developer credentials (default: `admin/admin`).

#### b. **Browse the API Catalog**
- The Developer Portal displays all available APIs that can be subscribed to.
- Browse or search for the API you wish to subscribe to using filters or the search bar.

#### c. **View API Details**
- Click on the API to view detailed information, including:
  - **API Overview**: General information, such as the API’s name, description, and version.
  - **API Documentation**: Endpoint details, usage guidelines, request/response formats, and authentication methods.
  - **Try Out**: You can try the API directly in the portal using the **Try it out** feature to test endpoints without subscribing.

#### d. **Subscribe to the API**
- After reviewing the API, click the **Subscribe** button.
- Select a **Subscription Tier** (throttling tier) that fits your use case. These tiers limit the number of requests you can make within a specified time (e.g., Bronze: 10,000 requests/day).
- Choose an existing application or create a new one during the subscription process.
  - Applications group multiple API subscriptions under a single entity, allowing easier token management.
- Confirm the subscription.

---

### 2. **Generating Access Tokens**

Once subscribed, you will need to generate an access token to authenticate API calls.

#### a. **Create an Application**
- If not done during subscription, create an application in the Developer Portal.
- Go to the **Applications** section and create a new application by providing a name and setting throttling limits.

#### b. **Generate Access Tokens**
- Inside the application view, there will be an option to generate access tokens. WSO2 API Manager supports OAuth2 tokens and API Keys.
  - **OAuth2 Tokens**: Select the scopes and grant types, such as **Password Grant**, **Client Credentials**, or **Authorization Code** to generate the token.
  - **API Keys**: An alternative authentication method where API keys are generated and attached to API requests instead of OAuth tokens.
- Once generated, the token can be used in the API requests' headers to authenticate the consumer.
  - Example:
    ```bash
    curl -X GET "https://<hostname>:8243/<api-context>/<api-resource>" -H "Authorization: Bearer <access-token>"
    ```

---

### 3. **Consuming APIs**

Once subscribed and with a token in hand, you can begin consuming the API from your applications. This typically involves sending HTTP requests to the API’s endpoints.

#### a. **Basic API Call Example**
   Here’s a sample `curl` command to consume an API using the access token generated earlier:
   ```bash
   curl -X GET "https://<hostname>:8243/<api-context>/<resource>" \
   -H "Authorization: Bearer <access-token>"
   ```

   In this example:
   - `<hostname>` is your WSO2 API Manager host (e.g., `api.example.com`).
   - `<api-context>` is the base path of the API (e.g., `/v1/weather`).
   - `<resource>` is the specific resource you want to access (e.g., `/current`).

#### b. **API Call with Query Parameters**
   If your API requires query parameters, you can include them in the request:
   ```bash
   curl -X GET "https://<hostname>:8243/v1/weather/current?city=London" \
   -H "Authorization: Bearer <access-token>"
   ```

#### c. **Handling Response**
   The API will return a response, typically in JSON format:
   ```json
   {
      "city": "London",
      "temperature": "15°C",
      "humidity": "80%"
   }
   ```

#### d. **Handling Errors**
   If you encounter an issue with the request, such as an invalid token, the API will return an error response:
   ```json
   {
      "error": "invalid_token",
      "error_description": "The access token expired"
   }
   ```
   In such cases, you may need to regenerate or refresh the token.

---

### 4. **API Keys as an Alternative to OAuth Tokens**

While OAuth2 tokens are more secure and offer fine-grained control via scopes, WSO2 API Manager also supports simpler **API Keys** for access.

#### a. **Generate an API Key**
- In the Developer Portal, go to your application and request an API Key for the subscribed API.
- The API Key will be displayed, and you can use it in your API requests.

#### b. **API Key Authentication Example**
   Here’s a sample API call using an API key:
   ```bash
   curl -X GET "https://<hostname>:8243/<api-context>/<resource>" \
   -H "apikey: <api-key>"
   ```

---

### 5. **Monitoring API Usage**

After consuming APIs, you may want to monitor how the API is being used.

#### a. **Analytics Dashboard**
- WSO2 API Manager integrates with **WSO2 API Analytics** to provide insights into API usage.
- You can monitor key metrics such as:
  - **Request Count**: Number of API calls made over a period.
  - **Latency**: Average response time for each API call.
  - **Throttling**: See how often APIs hit rate limits.
  - **Fault Count**: Number of failed requests (4xx and 5xx HTTP responses).

#### b. **Alerts and Notifications**
- Set up alerts to notify you when an API is heavily used or hitting throttling limits.
- This helps manage API consumption and ensure APIs perform optimally.

---

### 6. **Renewing and Revoking Access Tokens**

#### a. **Token Renewal**
- OAuth2 tokens typically have expiration times. To continue using the API, you may need to refresh or generate new tokens.
- Use the **refresh token** (if available) to generate a new access token without re-authenticating.

#### b. **Revoke Tokens**
- If you no longer want to allow a certain application to access the API, you can revoke the access token.
- This can be done from the Developer Portal under the **Applications** section.

---

### Conclusion

Subscribing to and consuming APIs in WSO2 API Manager is a straightforward process that ensures security, scalability, and efficient usage. With built-in tools for monitoring, analytics, and management, both API providers and consumers can maintain control and visibility over their API interactions.