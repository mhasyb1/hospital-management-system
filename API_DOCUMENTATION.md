# API Documentation

## Base URL

```
https://api.hms.example.com/api/v1
```

## Authentication

All API requests require JWT token in Authorization header:

```
Authorization: Bearer <JWT_TOKEN>
```

## Response Format

All responses follow this format:

```json
{
  "success": true/false,
  "data": {},
  "message": "Description",
  "timestamp": "2026-06-01T10:00:00Z"
}
```

---

## Patient Endpoints

### Register Patient

**Endpoint:** `POST /patients`

**Request Body:**
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "phone": "+1234567890",
  "dateOfBirth": "1990-01-15",
  "gender": "Male",
  "address": "123 Main St, City",
  "medicalHistory": [],
  "allergies": []
}
```

**Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "_id": "507f1f77bcf86cd799439011",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john@example.com"
  },
  "message": "Patient registered successfully"
}
```

### Get Patient by ID

**Endpoint:** `GET /patients/:id`

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "_id": "507f1f77bcf86cd799439011",
    "firstName": "John",
    "lastName": "Doe",
    "medicalHistory": [],
    "appointments": []
  }
}
```

### Update Patient

**Endpoint:** `PUT /patients/:id`

**Request Body:**
```json
{
  "firstName": "John",
  "address": "New Address"
}
```

**Response:** `200 OK`

### Delete Patient

**Endpoint:** `DELETE /patients/:id`

**Response:** `200 OK`
```json
{
  "success": true,
  "message": "Patient deleted successfully"
}
```

### Search Patients

**Endpoint:** `GET /patients/search?q=john`

**Response:** `200 OK`
```json
{
  "success": true,
  "data": [
    { "id": "...", "firstName": "John", "lastName": "Doe" }
  ]
}
```

---

## Doctor Endpoints

### Register Doctor

**Endpoint:** `POST /doctors`

**Request Body:**
```json
{
  "firstName": "Jane",
  "lastName": "Smith",
  "email": "jane@example.com",
  "specialization": "Cardiology",
  "licenseNumber": "MED123456",
  "experience": 10,
  "schedule": {
    "monday": "9AM-5PM",
    "tuesday": "9AM-5PM"
  }
}
```

**Response:** `201 Created`

### Get Doctor by ID

**Endpoint:** `GET /doctors/:id`

**Response:** `200 OK`

### Get Doctors by Specialization

**Endpoint:** `GET /doctors?specialization=Cardiology`

**Response:** `200 OK`
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439012",
      "firstName": "Jane",
      "specialization": "Cardiology"
    }
  ]
}
```

### Update Doctor

**Endpoint:** `PUT /doctors/:id`

**Request Body:** Similar to registration

**Response:** `200 OK`

---

## Appointment Endpoints

### Book Appointment

**Endpoint:** `POST /appointments`

**Request Body:**
```json
{
  "patientId": "507f1f77bcf86cd799439011",
  "doctorId": "507f1f77bcf86cd799439012",
  "appointmentDate": "2026-06-15",
  "appointmentTime": "2:00 PM",
  "reason": "Regular checkup"
}
```

**Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "_id": "507f1f77bcf86cd799439013",
    "status": "Scheduled",
    "appointmentDate": "2026-06-15"
  }
}
```

### Get Appointment

**Endpoint:** `GET /appointments/:id`

**Response:** `200 OK`

### Get Patient Appointments

**Endpoint:** `GET /appointments?patientId=:id`

**Response:** `200 OK`
```json
{
  "success": true,
  "data": [
    {
      "_id": "507f1f77bcf86cd799439013",
      "doctorId": "...",
      "appointmentDate": "2026-06-15",
      "status": "Scheduled"
    }
  ]
}
```

### Cancel Appointment

**Endpoint:** `DELETE /appointments/:id`

**Response:** `200 OK`
```json
{
  "success": true,
  "message": "Appointment cancelled successfully"
}
```

### Reschedule Appointment

**Endpoint:** `PUT /appointments/:id/reschedule`

**Request Body:**
```json
{
  "newDate": "2026-06-20",
  "newTime": "3:00 PM"
}
```

**Response:** `200 OK`

---

## Billing Endpoints

### Generate Bill

**Endpoint:** `POST /billing/generate`

**Request Body:**
```json
{
  "appointmentId": "507f1f77bcf86cd799439013",
  "services": [
    {"description": "Consultation", "amount": 100},
    {"description": "Lab Test", "amount": 50}
  ]
}
```

**Response:** `201 Created`
```json
{
  "success": true,
  "data": {
    "_id": "507f1f77bcf86cd799439014",
    "total": 150,
    "status": "Unpaid"
  }
}
```

### Get Bill

**Endpoint:** `GET /billing/:id`

**Response:** `200 OK`

### Process Payment

**Endpoint:** `POST /billing/:id/pay`

**Request Body:**
```json
{
  "paymentMethod": "Card",
  "amount": 150
}
```

**Response:** `200 OK`
```json
{
  "success": true,
  "data": {
    "billId": "507f1f77bcf86cd799439014",
    "status": "Paid",
    "paymentId": "PAY123456"
  }
}
```

---

## Error Responses

### 400 Bad Request
```json
{
  "success": false,
  "message": "Invalid input data",
  "errors": {
    "email": "Invalid email format"
  }
}
```

### 401 Unauthorized
```json
{
  "success": false,
  "message": "Authentication required",
  "code": "UNAUTHORIZED"
}
```

### 403 Forbidden
```json
{
  "success": false,
  "message": "Insufficient permissions"
}
```

### 404 Not Found
```json
{
  "success": false,
  "message": "Resource not found"
}
```

### 500 Server Error
```json
{
  "success": false,
  "message": "Internal server error",
  "code": "SERVER_ERROR"
}
```

---

**Last Updated:** June 1, 2026  
**API Version:** 1.0
