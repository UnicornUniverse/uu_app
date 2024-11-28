# API Integration Guide

This guide provides a step-by-step approach to interacting with the uuApp API, including authentication and request/response structure.

---

## Table of Contents

1. [Overview](#overview)
2. [Authentication](#authentication)
3. [API Request Structure](#api-request-structure)
4. [Making a Request](#making-a-request)
5. [Common Responses](#common-responses)

---

## Overview

All applications based on uuApp / uuDck must interact with the uuApp API to access data and perform operations. The API provides a set of endpoints for managing resources such as users, orders, and products.
URL is defined as `https://{baseuri}/{subapp}/{awid}/{useCase}`, sometimes alias is used and then the API is without subapp and awid part.

Example:
 - https://uuapp.plus4u.net/uu-webkit-maing02/d2a80094d8d24287befb333201f98edb/
   - baseuri: uuapp.plus4u.net
   - subapp: uu-webkit-maing02
   - awid: d2a80094d8d24287befb333201f98edb
   - useCase: / or /home or /about or /sys/uuAppWorkspace/load or /getProductLogo or /sys/uuAppWorkspace/productLogo/get
 - https://unicorn.com/
   - full URL: https://unicorn.com/
   - useCase: / or /home or /about or /sys/uuAppWorkspace/load or /getProductLogo or /sys/uuAppWorkspace/productLogo/get

---

## Authentication

The Authorized API requires Bearer Token authentication to secure API calls. You need to include the token in the `Authorization` header of each request.

### Obtaining a Bearer Token
1. Sign up or log in to your account at https://uuidentity.plus4u.net/.
2. Generate an API token from the **Show token** button.
3. **Keep your token secure; treat it as a password.**
4. It is possible to change scope to make it more secure or to use it for local development with `http://`

### Using the Bearer Token
Include the Bearer token in the `Authorization` header of your HTTP request as follows:
`Authorization: Bearer YOUR_ACCESS_TOKEN`

---

## API Request Structure

All API endpoints follow a consistent structure:

- **Base URL:** The root URL for all API requests: `https://unicorn.com/`
- **Endpoints:** Each endpoint represents a specific resource or operation. Example:
    - `/sys/uuAppWorkspace/load` for loading basic data about the workspace

### HTTP Methods
The API uses standard HTTP methods:
- `GET`: Retrieve data
- `POST`: Create a new resource, update an existing resource, or perform an action

### Headers
Every request must include:
```json
{
  "Authorization": "Bearer YOUR_ACCESS_TOKEN",
  "Content-Type": "application/json"
}
```

## Making a Request
Here’s an example of how to call the API to retrieve a content of page `/home`:

### cURL Example
```bash
curl -X GET https://unicorn.com/loadWebPage?code=home \
-H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
-H "Content-Type: application/json"
```

### JavaScript Example (using fetch)
```javascript
fetch('https://unicorn.com/loadWebPage?code=home', {
  method: 'GET',
  headers: {
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN',
    'Content-Type': 'application/json'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

## Common Responses
### Success Responses
200 OK: The request was successful, and the response contains the requested data.

### Error Responses
400 Bad Request: The request was invalid or malformed.
401 Unauthorized: The token is missing, expired, or invalid.
403 Forbidden: You lack the necessary permissions to access the resource.
404 Not Found: The requested resource does not exist.
500 Internal Server Error: An unexpected error occurred on the server.
