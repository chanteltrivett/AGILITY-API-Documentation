# AGILITY API Documentation

Welcome to AGILITY's API documentation. This guide provides detailed steps for using cURL to make requests to our API.

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

### 1: Obtain an Authentication Token

To authenticate, you will request an `id_token` by sending a POST request using cURL. This token will be required for all further API interactions.

#### cURL Command

Use the following cURL command to request an authentication token. Replace `YOUR_USERNAME` and `YOUR_PASSWORD` with your actual credentials:

```bash
curl -X POST 'https://cv-dev.b-yond.com/cv/auth/realms/predictiveai/protocol/openid-connect/token' \
     -H 'Content-Type: application/x-www-form-urlencoded' \
     -d 'grant_type=password&client_id=d0d8b0d806f9&username=YOUR_USERNAME&password=YOUR_PASSWORD&scope=openid'
```
#### Explanation

- `-X POST`: Specifies the POST request method.
- `-H 'Content-Type: application/x-www-form-urlencoded'`: Sets the content type for the request.
- `-d 'grant_type=password&client_id=d0d8b0d806f9&username=YOUR_USERNAME&password=YOUR_PASSWORD&scope=openid'`: The data payload for the request, including the grant type, client ID, username, password, and scope.

 #### Response

A successful request will return a JSON object containing several tokens, including the `id_token`. This token is essential for authenticating future requests.

#### Example response:

```json
{
    "access_token": "ACCESS_TOKEN_VALUE",
    "expires_in": 300,
    "refresh_expires_in": 1800,
    "refresh_token": "REFRESH_TOKEN_VALUE",
    "id_token": "YOUR_ID_TOKEN"
}
```
**Important**: Store these tokens securely. The `id_token` is especially important as it will be used to authenticate all subsequent API requests.

### 2: Use the Authentication Token

With the `id_token` obtained, include it in the header of all subsequent API requests for authentication.

## API Endpoints

### Retrieve Supported Services

This endpoint allows you to retrieve a list of services supported by AGILITY.

### 1: Run the cURL Command

To fetch the list of supported services, use the following cURL command. Replace `YOUR_ID_TOKEN` with the `id_token` obtained during authentication:

```bash
curl -X GET 'https://cv-dev.b-yond.com/cv/api/v1/services/?page=1&size=50' \
     -H 'Authorization: Bearer YOUR_ID_TOKEN' \
     -H 'accept: application/json'
```
### Explanation

- `-X GET`: Specifies the GET request method.
- `-H 'Authorization: Bearer YOUR_ID_TOKEN'`: Includes the `id_token` in the Authorization header.
- `-H 'accept: application/json'`: Indicates that the client expects a JSON response.

### Query Parameters

- `page`: (Default: 1) Specifies the page number of results.
- `size`: (Default: 50; Max: 100) Specifies the number of results per page.

## Start a New Analysis

To start a new network trace analysis, upload a trace file using the `POST 'https://cv-dev.b-yond.com/cv/api/v1/analysis/file'` endpoint.

### 1: Run the cURL Command

To start a new network trace analysis,upload a network trace file by using the following cURL command. Replace `myfile.pcap` with the path to your file and `YOUR_ID_TOKEN` with your authentication token:

```bash
curl -X POST 'https://cv-dev.b-yond.com/cv/api/v1/analysis/file' \
     -H 'Authorization: Bearer YOUR_ID_TOKEN' \
     -H 'accept: application/json' \
     -H 'Content-Type: multipart/form-data' \
     -F 'uploadFile=@myfile.pcap' \
     -F 'serviceKeys=volte'
```
#### Explanation

- **`-X POST`**: Specifies the POST request method.
- **`-H 'Authorization: Bearer YOUR_ID_TOKEN'`**: Includes the `id_token` in the Authorization header.
- **`-H 'accept: application/json'`**: Indicates that the client expects a JSON response.
- **`-H 'Content-Type: multipart/form-data'`**: Specifies that the request will include form data.
- **`-F 'uploadFile=@myfile.pcap'`**: The file to be uploaded. Replace `myfile.pcap` with your actual file path.
- **`-F 'serviceKeys=volte'`**: (Optional) Specifies the service keys for analysis. If unsure, leave it empty for auto-discovery.

## Fetch Analysis Results

Retrieve the results of a specific analysis using the analysis ID.

### 1. Run the cURL Command

To fetch analysis results, use the following cURL command. Replace `8599e936-19ee-4b13-a9ad-44fecadad9fe` with your specific analysis ID and `YOUR_ID_TOKEN` with your authentication token:

```bash
curl -X GET 'https://cv-dev.b-yond.com/cv/api/v1/analysis/8599e936-19ee-4b13-a9ad-44fecadad9fe/summary?page=1&size=50' \
     -H 'Authorization: Bearer YOUR_ID_TOKEN' \
     -H 'accept: application/json'
```
#### Explanation

- **`-X GET`**: Specifies the GET request method.
- **`-H 'Authorization: Bearer YOUR_ID_TOKEN'`**: Includes the `id_token` in the Authorization header.
- **`-H 'accept: application/json'`**: Indicates that the client expects a JSON response.

#### Query Parameters

- **`analysis_id`**: (Required) The unique identifier for the analysis.
- **`page`**: (Optional) (Default: 1) The page number of results.
- **`size`**: (Optional) (Default: 50; Max: 1000) The number of results per page.
