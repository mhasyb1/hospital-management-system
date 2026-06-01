# System Architecture

## Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │   HTML/CSS   │  │ JavaScript   │  │   UI/UX      │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────────┘
                           ↓ (HTTP/REST)
┌─────────────────────────────────────────────────────────┐
│                   API GATEWAY LAYER                      │
│  ┌────────────────────────────────────────────────────┐ │
│  │ Express.js Server with Routing & Middleware       │ │
│  └────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                 BUSINESS LOGIC LAYER                     │
│  ┌─────────────────────────────────────────────────┐   │
│  │  Controllers │ Services │ Utilities │ Validators│   │
│  │  - Patient Controller     - Auth Service       │   │
│  │  - Doctor Controller      - Email Service      │   │
│  │  - Appointment Controller - Notification Svc   │   │
│  │  - Billing Controller     - Calculation Svc    │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                   DATA ACCESS LAYER                      │
│  ┌─────────────────────────────────────────────────┐   │
│  │     Mongoose Models & Database Queries          │   │
│  │  - Patient Model      - Doctor Model            │   │
│  │  - Appointment Model  - Billing Model           │   │
│  │  - User Model         - Admin Model             │   │
│  └─────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                           ↓
┌─────────────────────────────────────────────────────────┐
│                  DATABASE LAYER                          │
│  ┌────────────────────────────────────────────────┐    │
│  │           MongoDB Database                     │    │
│  │  Collections: patients, doctors, appointments, │    │
│  │  billing, users, admin_logs                    │    │
│  └────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────┘
```

## Component Breakdown

### Frontend Layer
- **HTML/CSS**: User interface markup and styling
- **JavaScript**: Client-side logic and interactivity
- **UI Framework**: Responsive design implementation

### Backend Layer
- **Express.js**: Web server and routing framework
- **Controllers**: Handle incoming requests
- **Services**: Business logic implementation
- **Middleware**: Authentication, validation, error handling

### Database Layer
- **MongoDB**: NoSQL database for data storage
- **Mongoose**: ODM (Object Data Modeling) library
- **Collections**:
  - `patients`: Patient information and medical records
  - `doctors`: Doctor details and specializations
  - `appointments`: Appointment scheduling
  - `billing`: Invoice and payment records
  - `users`: System user accounts
  - `admin_logs`: Administrative activity logs

## Data Flow

### Patient Registration Flow
```
User Input (HTML Form)
    ↓
JavaScript Validation
    ↓
HTTP POST to /api/patients
    ↓
Express Route Handler
    ↓
Patient Controller
    ↓
Patient Service (Business Logic)
    ↓
Mongoose Model
    ↓
MongoDB Database
    ↓
Success Response
    ↓
JavaScript Updates UI
```

### Appointment Booking Flow
```
Doctor Selection & Date Input
    ↓
Availability Check (Service)
    ↓
Create Appointment Record
    ↓
Send Confirmation Email
    ↓
Update Calendar Display
    ↓
Store in Database
```

## Security Architecture

### Authentication
- JWT (JSON Web Tokens) for stateless authentication
- Password hashing with bcrypt
- Secure session management

### Authorization
- Role-based access control (RBAC)
- Endpoint-level authorization checks
- User permission verification

### Data Protection
- HTTPS encryption for data in transit
- Database encryption for sensitive data
- Input validation and sanitization

## Scalability Considerations

### Horizontal Scaling
- Stateless API design
- Load balancing support
- Distributed database architecture

### Vertical Scaling
- Database indexing on frequently queried fields
- Query optimization
- Caching strategies

## Error Handling

### Error Response Format
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable message",
    "details": "Technical details"
  }
}
```

### Error Types
- **Validation Errors** (400): Invalid input data
- **Authentication Errors** (401): Missing/invalid credentials
- **Authorization Errors** (403): Insufficient permissions
- **Not Found Errors** (404): Resource not found
- **Server Errors** (500): Internal server errors

## Performance Optimization

### Frontend Optimization
- Minified CSS and JavaScript
- Image optimization
- Lazy loading for heavy components
- Browser caching

### Backend Optimization
- Database indexing
- Query optimization
- API response caching
- Compression middleware

## Deployment Architecture

```
GitHub Repository
    ↓
GitHub Actions (CI/CD)
    ↓
Code Quality Checks
    ↓
Automated Testing
    ↓
Build & Package
    ↓
Deploy to Server
    ↓
Production Environment
```

---

**Last Updated:** June 1, 2026  
**Architect:** Mubarak Andarabi
