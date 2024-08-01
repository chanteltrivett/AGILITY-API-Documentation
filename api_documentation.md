# AGILITY API Documentation

Welcome to AGILITY'S API documentation, your guide to seamlessly integrating and utilizing our API for advanced network trace analysis.

## Contents

1. [Prerequisites](#prerequisites)
2. [Overview](#overview)
3. [API Base URL](#api-base-url)
4. [Authentication](#authentication)
    - [Request the Token](#request-the-token)
    - [Endpoint](#endpoint)
    - [Headers](#headers)
    - [Body](#body)
    - [Example cURL Request](#example-curl-request)
    - [Response](#response)
    - [Handling Expired Tokens](#handling-expired-tokens)
5. [API Endpoints](#predictive-ai-safeguard-api-endpoints)
    - [Retrieve Supported Services](#retrieve-supported-services)
        - [Endpoint](#endpoint-1)
        - [Parameters](#parameters)
        - [Example Request](#example-request)
    - [Start a New Analysis](#start-a-new-analysis)
        - [Endpoint](#endpoint-2)
        - [Request Body](#request-body)
        - [Example Request](#example-request-1)
    - [Fetch Analysis Results](#fetch-analysis-results)
        - [Endpoint](#endpoint-3)
        - [Parameters](#parameters-1)
        - [Example Request](#example-request-2)

## Prerequisites

Please get in touch with your account administrator to get your login credentials.

## Overview

The Predictive AI Safeguard API is designed to advance, optimize, and accelerate analysis on network traces. The software automates network predictions, and error resolutions by using ML to pinpoint the root causes for network failures. 

## API Base URL

Access the OpenAPI documentation via the base URL:

[http(s)://\<YOUR_PUBLIC_DN\>/cv/api/public/docs](https://predictive-ai-safeguard-community.b-yond.com/cv/api/public/docs)

## Authentication

Use the OAuth2 Password Flow to request an id_token.

### Request the Token

#### Endpoint

Request the authentication token by using the below-written POST request.

**POST /cv/auth/realms/predictiveai/protocol/openid-connect/token**

Then, provide your username, password, and client_id (public, provided as d0d8b0d806f9) to proceed to interact with the API.

#### Headers

- Content-Type: application/x-www-form-urlencoded

#### Body

- grant_type: password
- client_id: d0d8b0d806f9
- username: Your registered username
- password: Your password
- scope: openid

#### Example cURL Request

```bash
curl -X POST https://cv-dev.b-yond.com/cv/auth/realms/predictiveai/protocol/openid-connect/token \
     -H "Content-Type: application/x-www-form-urlencoded" \
     -d "grant_type=password&client_id=d0d8b0d806f9&username=YOUR_USERNAME&password=YOUR_PASSWORD&scope=openid"
```

#### Response

When you've successfully registered, you'll receive a JSON response containing the id_token, among other tokens.

- Use the value of YOUR_ID_TOKEN in your subsequent API requests as a Bearer Token for authentication.
- Use the value of YOUR_ID_TOKEN in your subsequent API requests as a Bearer Token for authentication.

```json
{
    "access_token": "ACCESS_TOKEN_VALUE",
    "expires_in": 300,
    "refresh_expires_in": 1800,
    "refresh_token": "REFRESH_TOKEN_VALUE",
    "id_token": "YOUR_ID_TOKEN",
    // ... other tokens
}
```

**Note:** Keep tokens secure and avoid exposing them in insecure locations.

### Handling Expired Tokens

If your access token expires, you'll be redirected to the login page. Follow these steps to handle expired tokens:

1. Make a refresh token request:

    ```bash
    POST /cv/auth/realms/predictiveai/protocol/openid-connect/token
    Content-Type: application/x-www-form-urlencoded

    grant_type=refresh_token
    &refresh_token=[Your Refresh Token]
    &client_id=d0d8b0d806f9
    ```

2. If the refresh token is valid, you'll receive a new id_token.

3. Update your authorization using the new access token.

**Note:** Securely store and manage the refresh token.

## Endpoints

### Retrieve Supported Services

#### Endpoint

To fetch a list of supported services, use the below-written GET request.

**GET /cv/api/v1/services/**


#### Parameters

- page: Specify the page number. (Default: 1)
- size: Specify the number of results per page. (Default: 50; Maximum: 100)

#### Example Request

```bash
curl -X 'GET' \
  'https://cv-dev.b-yond.com/cv/api/v1/services/?page=1&size=50' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer YOUR_ID_TOKEN'
```

### Start a New Analysis

#### Endpoint

To start an analysis use the below-written Post request to upload a supported network trace file.

**POST /cv/api/v1/analysis/file**


#### Request Body

- uploadFile: Upload your network trace file (available locally).
- serviceKeys: (Optional) List of service keys for analysis. If you're unsure of the applicable service keys, leave the service keys field empty for service auto-discovery.

#### Example Request

```bash
curl -X 'POST' \
  'https://cv-dev.b-yond.com/cv/api/v1/analysis/file' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer YOUR_ID_TOKEN' \
  -H 'Content-Type: multipart/form-data' \
  -F 'uploadFile=@myfile.pcap' \
  -F 'serviceKeys=volte'
```

### Fetch Analysis Results

#### Endpoint

Use the below-written GET request to retrieve analysis results.

**GET /cv/api/v1/analysis/{analysis_id}/summary**


#### Parameters

- analysis_id: The ID of the analysis (received from the previous step).
- page: (Optional) Specify the page number. (Default: 1)
- size: (Optional) Specify the number of results per page. (Default: 50; Maximum: 1000)

#### Example Request

```bash
curl -X 'GET' \
  'https://cv-dev.b-yond.com/cv/api/v1/analysis/8599e936-19ee-4b13-a9ad-44fecadad9fe/summary?page=1&size=50' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer YOUR_ID_TOKEN'
```
# AGILITY API Documentation

Welcome to AGILITY's API documentation. This guide provides detailed steps for integrating and using our API for advanced network trace analysis, using cURL for making requests.

## Contents

1. [Prerequisites](#prerequisites)
2. [Overview](#overview)
3. [API Base URL](#api-base-url)
4. [Authentication](#authentication)
    - [Step 1: Obtain an Authentication Token](#step-1-obtain-an-authentication-token)
    - [Step 2: Use the Authentication Token](#step-2-use-the-authentication-token)
5. [API Endpoints](#api-endpoints)
    - [Retrieve Supported Services](#retrieve-supported-services)
    - [Start a New Analysis](#start-a-new-analysis)
    - [Fetch Analysis Results](#fetch-analysis-results)

## Prerequisites

To access the API, you need to have your login credentials. Contact your account administrator to obtain these credentials.

## Overview

The AGILITY API provides tools for automating network trace analysis, leveraging machine learning to diagnose network issues. The API facilitates optimizing and accelerating network predictions and error resolutions.

## API Base URL

Access the API endpoints through the following base URL:

`https://<YOUR_PUBLIC_DN>/cv/api/public/docs`

## Authentication

Before you can use the AGILITY API, you must authenticate yourself by obtaining an `id_token`. This token will authorize your API requests.

### Step 1: Obtain an Authentication Token

To authenticate, you will request an `id_token` by sending a POST request using cURL. This token will be required for all further API interactions.

#### cURL Command

Use the following cURL command to request an authentication token. Replace `YOUR_USERNAME` and `YOUR_PASSWORD` with your actual credentials:

```bash
curl -X POST 'https://cv-dev.b-yond.com/cv/auth/realms/predictiveai/protocol/openid-connect/token' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     -d 'grant_type=password&client_id=d0d8b0d806f9&username=YOUR_USERNAME&password=YOUR_PASSWORD&scope=openid'
** ## Explanation

- `-X POST`: Specifies the POST request method.
- `-H 'Content-Type: application/x-www-form-urlencoded'`: Sets the content type for the request.
- `-d 'grant_type=password&client_id=d0d8b0d806f9&username=YOUR_USERNAME&password=YOUR_PASSWORD&scope=openid'`: The data payload for the request, including the grant type, client ID, username, password, and scope.

 ## Response

A successful request will return a JSON object containing several tokens, including the `id_token`. This token is essential for authenticating future requests.

### Example response:

```json
{
    "access_token": "ACCESS_TOKEN_VALUE",
    "expires_in": 300,
    "refresh_expires_in": 1800,
    "refresh_token": "REFRESH_TOKEN_VALUE",
    "id_token": "YOUR_ID_TOKEN"
}
**Important**: Store these tokens securely. The `id_token` is especially important as it will be used to authenticate all subsequent API requests.

## Step 2: Use the Authentication Token

With the `id_token` obtained, include it in the header of all subsequent API requests for authentication.

## API Endpoints

### Retrieve Supported Services

This endpoint allows you to retrieve a list of services supported by AGILITY.

#### cURL Command

To fetch the list of supported services, use the following cURL command. Replace `YOUR_ID_TOKEN` with the `id_token` obtained during authentication:

```bash
curl -X GET 'https://cv-dev.b-yond.com/cv/api/v1/services/?page=1&size=50' \
     -H 'Authorization: Bearer YOUR_ID_TOKEN' \
     -H 'accept: application/json'
## Explanation

- `-X GET`: Specifies the GET request method.
- `-H 'Authorization: Bearer YOUR_ID_TOKEN'`: Includes the `id_token` in the Authorization header.
- `-H 'accept: application/json'`: Indicates that the client expects a JSON response.

## Query Parameters

- `page`: (Default: 1) Specifies the page number of results.
- `size`: (Default: 50; Max: 100) Specifies the number of results per page.

## Start a New Analysis

To start a new network trace analysis, upload a trace file using this endpoint.

### cURL Command

Upload a network trace file by using the following cURL command. Replace `myfile.pcap` with the path to your file and `YOUR_ID_TOKEN` with your authentication token:

```bash
curl -X POST 'https://cv-dev.b-yond.com/cv/api/v1/analysis/file' \
     -H 'Authorization: Bearer YOUR_ID_TOKEN' \
     -H 'accept: application/json' \
     -H 'Content-Type: multipart/form-data' \
     -F 'uploadFile=@myfile.pcap' \
     -F 'serviceKeys=volte'
