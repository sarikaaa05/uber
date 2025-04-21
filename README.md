# API Documentation

## User Registration Endpoint

### POST /users/register

Register a new user in the system.

#### Request Body

```json
{
  "username": "string",
  "email": "string",
  "password": "string",
  "phone": "string"
}
```

#### Required Fields

- `username`: User's display name (3-30 characters)
- `email`: Valid email address
- `password`: Password (minimum 6 characters)
- `phone`: Valid phone number

#### Response Status Codes

- `201 Created`: User successfully registered
- `400 Bad Request`: Invalid input data
- `409 Conflict`: Email already exists
- `500 Internal Server Error`: Server error

#### Example Response (Success)

```json
{
  "status": "success",
  "message": "User registered successfully",
  "data": {
    "id": "uuid",
    "username": "john_doe",
    "email": "john@example.com"
  }
}
```

#### Example Response (Error)

```json
{
  "status": "error",
  "message": "Email already exists"
}
```

## User Login Endpoint

### POST /users/login

Authenticate a user and receive an access token.

#### Request Body

```json
{
  "email": "string",
  "password": "string"
}
```

#### Required Fields

- `email`: Registered email address
- `password`: User's password

#### Response Status Codes

- `200 OK`: Login successful
- `400 Bad Request`: Invalid input data
- `401 Unauthorized`: Invalid credentials
- `500 Internal Server Error`: Server error

#### Example Response (Success)

```json
{
  "token": "jwt_token_string",
  "user": {
    "id": "uuid",
    "email": "john@example.com",
    "username": "john_doe"
  }
}
```

#### Example Response (Error)

```json
{
  "message": "Invalid email or password"
}
```

## Get User Profile Endpoint

### GET /users/profile

Retrieve the authenticated user's profile information.

#### Headers Required

- `Authorization`: Bearer token received from login

#### Response Status Codes

- `200 OK`: Profile retrieved successfully
- `401 Unauthorized`: Invalid or missing token
- `500 Internal Server Error`: Server error

#### Example Response (Success)

```json
{
  "id": "uuid",
  "email": "john@example.com",
  "username": "john_doe",
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  }
}
```

## User Logout Endpoint

### GET /users/logout

Logout the currently authenticated user.

#### Headers Required

- `Authorization`: Bearer token received from login

#### Response Status Codes

- `200 OK`: Logout successful
- `401 Unauthorized`: Invalid or missing token
- `500 Internal Server Error`: Server error

#### Example Response (Success)

```json
{
  "message": "Logged out successfully"
}
```
