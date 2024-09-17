Here are working examples for creating various types of APIs using **WSO2 API Manager**:

---

## 1. **Design a New REST API**: Create an API from Scratch by Defining its Resources

### Steps:

1. **Login to WSO2 API Manager Publisher**:
   - Go to `https://<your-server-ip>:9443/publisher`.
   - Login with the default credentials (**admin** / **admin**).

2. **Create a New REST API**:
   - Click on **Create API** and select **Design a New REST API**.
   - Fill in the **Basic Information**:
     - **Name**: `EmployeeAPI`
     - **Context**: `/employees`
     - **Version**: `v1`
     - **Endpoint**: `https://mock-server.com/employees`
   - Click **Next**.

3. **Define Resources**:
   - Add a new resource for **GET** `/employees/{id}`.
     - **Resource Path**: `/employees/{id}`
     - **HTTP Verb**: `GET`
     - **Summary**: `Fetch employee by ID`
   - Add another resource for **POST** `/employees`.
     - **Resource Path**: `/employees`
     - **HTTP Verb**: `POST`
     - **Summary**: `Add a new employee`
   - Click **Next**.

4. **Select Security Options**:
   - Select the authentication method (e.g., OAuth2).
   - You can also enable **API Throttling** here.

5. **Deploy the API**:
   - Click **Deploy**.
   - The API will be deployed and available in the **API Gateway** for consumption.

6. **Publish the API**:
   - After deployment, click **Publish** to make the API available for subscriptions.

### Example cURL Request (After publishing):
```bash
curl -X GET "https://<gateway-host>/employees/123" -H "Authorization: Bearer <access-token>"
```

---

## 2. **Import OpenAPI Specification**: Upload an OpenAPI (Swagger) Definition to Automatically Create the API

### Steps:

1. **Login to WSO2 API Manager Publisher**:
   - Go to `https://<your-server-ip>:9443/publisher`.

2. **Create an API from an OpenAPI (Swagger)**:
   - Click on **Create API** and select **Import OpenAPI**.
   - Upload your OpenAPI file or provide a URL to the OpenAPI specification. For example:
     - **URL**: `https://petstore.swagger.io/v2/swagger.json`
   - Click **Next**.

3. **Configure API**:
   - The OpenAPI specification will automatically populate fields such as API name, version, and context.
     - **Name**: `PetstoreAPI`
     - **Context**: `/petstore`
     - **Version**: `v1`
   - You can review the resources imported from the OpenAPI definition, including the paths and HTTP methods.

4. **Deploy and Publish**:
   - Deploy and publish the API by following the same steps as in the previous section.

### Example OpenAPI (Swagger) JSON snippet:
```json
{
  "swagger": "2.0",
  "info": {
    "version": "1.0.0",
    "title": "Swagger Petstore"
  },
  "paths": {
    "/pet": {
      "post": {
        "summary": "Add a new pet to the store",
        "operationId": "addPet",
        "parameters": [],
        "responses": {
          "405": {
            "description": "Invalid input"
          }
        }
      }
    }
  }
}
```

---

## 3. **SOAP or WebSocket API**: Create SOAP or WebSocket APIs

### SOAP API

1. **Login to WSO2 API Manager Publisher**.

2. **Create a New SOAP API**:
   - Click on **Create API** and select **SOAP API**.
   - Provide the **WSDL URL** of the SOAP service.
     - **Example**: `http://www.dneonline.com/calculator.asmx?wsdl`
   - Fill in the **Basic Information**:
     - **Name**: `CalculatorAPI`
     - **Context**: `/calculator`
     - **Version**: `v1`

3. **Deploy and Publish**:
   - Once the WSDL is loaded, WSO2 API Manager will auto-generate the SOAP operations.
   - Deploy and publish the API.

### WebSocket API

1. **Login to WSO2 API Manager Publisher**.

2. **Create a New WebSocket API**:
   - Click on **Create API** and select **WebSocket API**.
   - Provide the **WebSocket URL**:
     - **Example**: `ws://echo.websocket.org`
   - Fill in the **Basic Information**:
     - **Name**: `EchoAPI`
     - **Context**: `/echo`
     - **Version**: `v1`

3. **Deploy and Publish**:
   - Deploy the WebSocket API.

### Example WebSocket Client (JavaScript):
```javascript
let socket = new WebSocket("wss://<gateway-host>/echo");
socket.onmessage = function(event) {
  console.log(event.data);
};
socket.send("Hello WebSocket!");
```

---

## 4. **Service Catalog**: Import a Service from the Service Catalog (for Microservices Discovery)

### Steps:

1. **Register the Microservice in the Service Catalog**:
   - Login to the **Service Catalog** in WSO2 API Manager.
   - Add the microservice information to the service catalog. For example:
     - **Service Name**: `UserService`
     - **Type**: `HTTP`
     - **Endpoint**: `http://user-service:8080`

2. **Login to WSO2 API Manager Publisher**.

3. **Import Microservice from Service Catalog**:
   - Click on **Create API** and select **Import from Service Catalog**.
   - Select the **UserService** microservice from the catalog.
   - The API Manager will automatically pull the details of the microservice.

4. **Define Resources**:
   - Add any required resources for the microservice.
     - Example resource:
       - **Path**: `/users/{id}`
       - **HTTP Method**: `GET`

5. **Deploy and Publish**:
   - Deploy and publish the API.

---

### Conclusion

These examples show how you can use **WSO2 API Manager** to create and manage various types of APIs, including REST, SOAP, WebSocket, and microservices. Depending on your use case, you can design APIs from scratch, import existing API definitions (OpenAPI/Swagger), or integrate microservices using the Service Catalog.