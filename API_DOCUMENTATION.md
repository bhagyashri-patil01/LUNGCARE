# API Documentation

## Base URL
```
http://localhost:5000/api
```

## Authentication

All endpoints except `/auth/register` and `/auth/login` require JWT token:
```
Authorization: Bearer <token>
```

## Endpoints

### Authentication

#### Register User
```http
POST /auth/register
Content-Type: application/json

{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "securepassword123",
  "full_name": "John Doe"
}

Response: 201 Created
{
  "user": {
    "id": 1,
    "username": "john_doe",
    "email": "john@example.com",
    "full_name": "John Doe",
    "is_admin": false
  },
  "token": "eyJhbGc..."
}
```

#### Login User
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securepassword123"
}

Response: 200 OK
{
  "user": {...},
  "token": "eyJhbGc..."
}
```

#### Get Profile
```http
GET /auth/profile
Authorization: Bearer <token>

Response: 200 OK
{
  "id": 1,
  "username": "john_doe",
  "email": "john@example.com",
  "full_name": "John Doe",
  "avatar_url": "https://...",
  "is_admin": false
}
```

#### Update Profile
```http
PUT /auth/profile
Authorization: Bearer <token>
Content-Type: application/json

{
  "full_name": "John Updated",
  "avatar_url": "https://example.com/avatar.jpg"
}

Response: 200 OK
```

### Dashboard

#### Create Data
```http
POST /dashboard/data
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Monthly Sales",
  "data_type": "chart",
  "description": "Sales data for Q1 2024",
  "data_values": {
    "months": ["Jan", "Feb", "Mar"],
    "values": [100, 150, 200]
  }
}

Response: 201 Created
```

#### Get User Data
```http
GET /dashboard/data
Authorization: Bearer <token>

Response: 200 OK
[
  {
    "id": 1,
    "user_id": 1,
    "title": "Monthly Sales",
    "data_type": "chart",
    "description": "...",
    "data_values": {...},
    "created_at": "2024-01-15T10:30:00Z"
  }
]
```

#### Update Data
```http
PUT /dashboard/data/1
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Updated Title",
  "description": "New description",
  "data_values": {...}
}
```

#### Delete Data
```http
DELETE /dashboard/data/1
Authorization: Bearer <token>

Response: 200 OK
```

#### Search Data
```http
GET /dashboard/search?query=sales
Authorization: Bearer <token>

Response: 200 OK
[...]
```

### Notifications

#### Get Notifications
```http
GET /notifications
Authorization: Bearer <token>

Response: 200 OK
[
  {
    "id": 1,
    "user_id": 1,
    "title": "New Upload",
    "message": "File uploaded successfully",
    "type": "success",
    "is_read": false,
    "created_at": "2024-01-15T10:30:00Z"
  }
]
```

#### Create Notification
```http
POST /notifications
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Alert",
  "message": "This is an important message",
  "type": "info"
}
```

#### Mark as Read
```http
PUT /notifications/1
Authorization: Bearer <token>

Response: 200 OK
```

#### Delete Notification
```http
DELETE /notifications/1
Authorization: Bearer <token>
```

### Files

#### Upload File
```http
POST /files/upload
Authorization: Bearer <token>
Content-Type: multipart/form-data

FormData:
- file: [binary file data]

Response: 201 Created
{
  "id": 1,
  "user_id": 1,
  "file_name": "document.pdf",
  "file_path": "uploads/...",
  "file_size": 1024000,
  "file_type": "application/pdf",
  "uploaded_at": "2024-01-15T10:30:00Z"
}
```

#### Get User Files
```http
GET /files
Authorization: Bearer <token>

Response: 200 OK
[...]
```

#### Delete File
```http
DELETE /files/1
Authorization: Bearer <token>
```

### Users (Admin Only)

#### Get All Users
```http
GET /users
Authorization: Bearer <admin_token>

Response: 200 OK
[...]
```

#### Delete User
```http
DELETE /users/1
Authorization: Bearer <admin_token>
```

## Error Responses

### 400 Bad Request
```json
{
  "error": "Missing required fields"
}
```

### 401 Unauthorized
```json
{
  "error": "Invalid credentials"
}
```

### 403 Forbidden
```json
{
  "error": "Admin access required"
}
```

### 404 Not Found
```json
{
  "error": "Resource not found"
}
```

### 500 Internal Server Error
```json
{
  "error": "Something went wrong!"
}
```

## Rate Limiting

Currently not implemented. Consider adding for production.

## WebSocket Events (Socket.io)

### Connect
```javascript
socket.on('connect', () => {
  socket.emit('join_room', userId);
});
```

### Receive Notification
```javascript
socket.on('new_notification', (notification) => {
  // Handle new notification
});
```

### Send Notification
```javascript
socket.emit('send_notification', {
  userId: 1,
  title: 'Alert',
  message: 'Important message'
});
```
