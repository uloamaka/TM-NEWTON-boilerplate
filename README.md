# Comprehensive Boilerplate API Design (Team Newton)
- Link to API design doc:
https://documentatioin.s3.amazonaws.com/index.html

- Link to DB design:
 https://dbdiagram.io/d/TM-NEWTON-669120579939893daec4cfa5

## 1. Introduction

This Comprehensive Boilerplate API provides a robust set of endpoints for building a feature-rich web application. This document outlines the API's structure, main features, and key endpoints, including request and response formats.

## 2. API Overview

- **Version**: 1.0.0
- **Base URL**: https://api.example.com/v1

## 3. Key Features

1. User Authentication
2. Messaging System
3. Organization Management
4. Blog Post Handling
5. Multi-Gateway Payment Processing
6. Notification System
7. Invite System
8. Content Editing

## 4. Authentication

The API uses API key authentication. All authenticated endpoints require a valid API key in the Authorization header, prefixed with 'Bearer '.

## 5. Main Endpoints and Request/Response Structures

### 5.1 Authentication

#### 5.1.1 Register a new user

- **Endpoint**: POST `/auth/register`
- **Request Body**:
  ```json
  {
    "username": "string",
    "email": "string",
    "password": "string",
    "firstName": "string",
    "lastName": "string"
  }
  ```
- **Response Body** (201 Created):
  ```json
  {
    "userId": "string",
    "username": "string",
    "email": "string",
    "firstName": "string",
    "lastName": "string",
    "avatarUrl": "string",
    "createdAt": "string",
    "updatedAt": "string"
  }
  ```

#### 5.1.2 Login a user

- **Endpoint**: POST `/auth/login`
- **Request Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Response Body** (200 OK):
  ```json
  {
    "token": "string",
    "expiresAt": "string"
  }
  ```

### 5.2 Messaging

#### 5.2.1 Send a message

- **Endpoint**: POST `/messages`
- **Request Body**:
  ```json
  {
    "senderId": "string",
    "recipientId": "string",
    "subject": "string",
    "body": "string"
  }
  ```
- **Response Body** (201 Created):
  ```json
  {
    "messageId": "string",
    "sentAt": "string"
  }
  ```

### 5.3 Organizations

#### 5.3.1 Create a new organization

- **Endpoint**: POST `/organizations`
- **Request Body**:
  ```json
  {
    "orgName": "string",
    "orgEmail": "string",
    "orgLogoUrl": "string",
    "location": "string",
    "description": "string"
  }
  ```
- **Response Body** (201 Created):
  ```json
  {
    "orgId": "string",
    "orgName": "string",
    "orgEmail": "string",
    "createdAt": "string"
  }
  ```

### 5.4 Blogs

#### 5.4.1 Create a new blog post

- **Endpoint**: POST `/blogs`
- **Request Body**:
  ```json
  {
    "title": "string",
    "content": "string",
    "authorId": "string",
    "categories": ["string"],
    "tags": ["string"]
  }
  ```
- **Response Body** (201 Created):
  ```json
  {
    "postId": "string",
    "title": "string",
    "authorId": "string",
    "publishedAt": "string",
    "updatedAt": "string"
  }
  ```

#### 5.4.2 Get all blog posts

- **Endpoint**: GET `/blogs`
- **Query Parameters**:
  - `page`: integer
  - `limit`: integer
  - `author`: string
  - `category`: string
  - `fromDate`: string (date)
  - `toDate`: string (date)
- **Response Body** (200 OK):
  ```json
  {
    "posts": [
      {
        "postId": "string",
        "title": "string",
        "authorId": "string",
        "publishedAt": "string",
        "updatedAt": "string"
      }
    ],
    "total": "integer",
    "page": "integer",
    "limit": "integer"
  }
  ```

### 5.5 Payments

#### 5.5.1 Process a Stripe payment

- **Endpoint**: POST `/payments/stripe`
- **Request Body**:
  ```json
  {
    "amount": "integer",
    "currency": "string",
    "description": "string",
    "stripeToken": "string"
  }
  ```
- **Response Body** (200 OK):
  ```json
  {
    "status": "string",
    "amount": "integer",
    "currency": "string",
    "transactionId": "string",
    "description": "string",
    "createdAt": "string"
  }
  ```

### 5.6 Notifications

#### 5.6.1 Get notifications for dashboard

- **Endpoint**: GET `/notifications`
- **Query Parameters**:
  - `page`: integer
  - `limit`: integer
  - `type`: string
  - `fromDate`: string (date)
  - `toDate`: string (date)
- **Response Body** (200 OK):
  ```json
  {
    "notifications": [
      {
        "id": "string",
        "userId": "string",
        "message": "string",
        "type": "string",
        "isRead": "boolean",
        "createdAt": "string"
      }
    ],
    "total": "integer",
    "page": "integer",
    "limit": "integer"
  }
  ```

### 5.7 Invites

#### 5.7.1 Send an invite link

- **Endpoint**: POST `/invites`
- **Request Body**:
  ```json
  {
    "email": "string",
    "orgId": "string",
    "role": "string"
  }
  ```
- **Response Body** (200 OK):
  ```json
  {
    "status": "string",
    "message": "string",
    "inviteId": "string",
    "expiresAt": "string"
  }
  ```

### 5.8 Content

#### 5.8.1 Edit content

- **Endpoint**: PUT `/content`
- **Request Body**:
  ```json
  {
    "contentId": "string",
    "newContent": "string",
    "contentType": "string",
    "version": "integer"
  }
  ```
- **Response Body** (200 OK):
  ```json
  {
    "status": "string",
    "contentId": "string",
    "version": "integer",
    "updatedAt": "string"
  }
  ```

## 6. Error Handling

The API uses standard HTTP status codes and provides detailed error responses:

```json
{
  "code": "string",
  "message": "string",
  "details": {
    "field": "string",
    "issue": "string"
  }
}
```

Common error responses include:
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 429 Too Many Requests
- 500 Internal Server Error

## 7. Pagination

List endpoints support pagination using query parameters:
- `page`: The page number (default: 1)
- `limit`: Number of items per page (default varies by endpoint)

## 8. Security

- Uses HTTPS for all communications
- Implements API key authentication
- Supports social login and magic link authentication

## 9. Rate Limiting

The API implements rate limiting to prevent abuse. Clients exceeding the rate limit will receive a 429 Too Many Requests response.

## 10. Documentation

Detailed API documentation is available at https://documentatioin.s3.amazonaws.com/index.html


# Contributors

Thanks to the following people who have contributed to this project:

- [@Chukwuji Matthew Olisenekwu](https://github.com/Mattiechuks)
- [@Akintola Olamilekan](https://github.com/horlami228)
- [@Uche Ali](https://github.com/SolowiseCv)
- [@onlyoneuche](github.com/onlyoneuche)
- [@Uloamaka](https://github.com/uloamaka)