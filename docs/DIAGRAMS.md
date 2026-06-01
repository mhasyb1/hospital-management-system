# System Diagrams

## 1. Use Case Diagram

```
                    ┌─────────────────┐
                    │    Hospital     │
                    │ Management      │
                    │ System          │
                    └─────────────────┘
                          ▲
        ┌─────────────────┼─────────────────┐
        │                 │                 │
    ┌───▼────┐        ┌───▼────┐      ┌───▼────┐
    │ Patient │        │ Doctor │      │  Admin │
    └────┬────┘        └────┬───┘      └────┬───┘
         │                  │               │
         ├─ Register        ├─ View Schedule├─ Manage Users
         ├─ Book Appt       ├─ Update       ├─ Generate Reports
         ├─ View History    │   Availability├─ System Config
         ├─ Pay Bills       ├─ View Appts   └─ Audit Logs
         └─ View Records    └─ Create Bills

```

## 2. Data Flow Diagram

### Patient Registration Flow
```
User Form Input
    │
    ▼
JavaScript Validation
    │ (Valid?)
    ├─Yes──────────────┐
    │                  │
    │              HTTP POST
    │              /api/patients
    │                  │
    │                  ▼
    │          Express Server
    │                  │
    │                  ▼
    │          Patient Controller
    │                  │
    │                  ▼
    │          Patient Service
    │          (Business Logic)
    │                  │
    │                  ▼
    │          MongoDB
    │          Patients Collection
    │                  │
    │                  ▼
    │          Send Email
    │                  │
    │                  ▼
    │          Success Response
    │                  │
    │                  ▼
    │          Update UI
    │
    └─No──── Show Error Message
```

### Appointment Booking Flow
```
Select Doctor
    │
    ▼
Check Availability
    │
    ▼
Select Date/Time
    │
    ▼
Confirm Booking
    │
    ▼
Create Appointment Record
    │
    ▼
Generate Bill
    │
    ▼
Send Confirmation Email
    │
    ▼
Update Patient Calendar
    │
    ▼
Update Doctor Schedule
    │
    ▼
Success Notification
```

## 3. Entity Relationship Diagram (ERD)

```
PATIENTS
┌──────────────────┐
│ _id (PK)         │
│ firstName        │
│ lastName         │
│ email (UNIQUE)   │
│ phone            │
│ dateOfBirth      │
│ gender           │
│ address          │
│ medicalHistory   │
│ allergies        │
└──────────────────┘
        │
        │ 1:N
        │
        ▼
APPOINTMENTS
┌──────────────────┐
│ _id (PK)         │
│ patientId (FK)   │─┐
│ doctorId (FK)    │─┼─┐
│ appointmentDate  │ │ │
│ appointmentTime  │ │ │
│ reason           │ │ │
│ status           │ │ │
└──────────────────┘ │ │
        │            │ │
        │ 1:N        │ │
        ▼            │ │
BILLING              │ │
┌──────────────────┐ │ │
│ _id (PK)         │ │ │
│ appointmentId    │─┘ │
│ patientId (FK)   │───┘
│ doctorId (FK)    │
│ billDate         │
│ total            │
│ status           │
└──────────────────┘

        DOCTORS
    ┌──────────────────┐
    │ _id (PK)         │
    │ firstName        │
    │ lastName         │
    │ email (UNIQUE)   │
    │ specialization   │
    │ licenseNumber    │
    │ experience       │
    │ schedule         │
    │ consultationFee  │
    └──────────────────┘

        USERS
    ┌──────────────────┐
    │ _id (PK)         │
    │ email (UNIQUE)   │
    │ password (hash)  │
    │ role             │
    │ isActive         │
    └──────────────────┘

    ADMIN_LOGS
    ┌──────────────────┐
    │ _id (PK)         │
    │ userId (FK)      │
    │ action           │
    │ targetModel      │
    │ targetId         │
    │ timestamp        │
    └──────────────────┘
```

## 4. System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                          │
│     ┌───────────────────────────────────────────────┐   │
│     │    HTML/CSS + JavaScript (Frontend)           │   │
│     │    ├─ Patient Dashboard                       │   │
│     │    ├─ Doctor Portal                           │   │
│     │    ├─ Admin Panel                             │   │
│     │    └─ Appointment Calendar                    │   │
│     └───────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                         ▲
                         │ HTTP/HTTPS
                         ▼
┌─────────────────────────────────────────────────────────┐
│                 API GATEWAY LAYER                        │
│     ┌───────────────────────────────────────────────┐   │
│     │  Express.js Server (Node.js)                  │   │
│     │  ├─ Routes (/patients, /doctors, /appts)     │   │
│     │  ├─ Middleware (Auth, Validation)             │   │
│     │  └─ Error Handling                            │   │
│     └───────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                         ▲
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│              BUSINESS LOGIC LAYER                        │
│     ┌──────────────┐  ┌──────────────┐                  │
│     │ Controllers  │  │ Services     │                  │
│     │              │  │              │                  │
│     │ PatientCtrl  │  │ AuthService  │                  │
│     │ DoctorCtrl   │  │ EmailService │                  │
│     │ ApptCtrl     │  │ BillingServ  │                  │
│     │ BillingCtrl  │  │ NotifService │                  │
│     └──────────────┘  └──────────────┘                  │
└─────────────────────────────────────────────────────────┘
                         ▲
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                DATA ACCESS LAYER                         │
│     ┌───────────────────────────────────────────────┐   │
│     │     Mongoose Models & Queries                 │   │
│     │     ├─ PatientModel                           │   │
│     │     ├─ DoctorModel                            │   │
│     │     ├─ AppointmentModel                       │   │
│     │     ├─ BillingModel                           │   │
│     │     ├─ UserModel                              │   │
│     │     └─ AdminLogModel                          │   │
│     └───────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                         ▲
                         │
                         ▼
┌─────────────────────────────────────────────────────────┐
│                   DATABASE LAYER                         │
│     ┌───────────────────────────────────────────────┐   │
│     │        MongoDB Database                       │   │
│     │        (hospital-ms collection)               │   │
│     └───────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
```

## 5. Deployment Architecture

```
GitHub Repository
    │
    ├─ Push to main
    │
    ▼
GitHub Actions CI/CD
    │
    ├─ Run Tests
    │
    ├─ Code Analysis
    │
    └─ Build Project
            │
            ▼
    Staging Environment
    (Testing Server)
            │
            ├─ Manual Testing
            │
            └─ Performance Testing
                    │
                    ▼
    Production Deployment
    ┌─────────────────────┐
    │  Load Balancer      │
    │  (Nginx)            │
    └──────┬──────────────┘
           │
    ┌──────┴──────┬──────────┐
    │             │          │
    ▼             ▼          ▼
Node.js App 1  App 2      App 3
(pm2 process)  (cluster)
    │             │          │
    └──────┬──────┴──────────┘
           │
           ▼
    MongoDB Database
    (Replicated)
```

## 6. State Diagram - Appointment Lifecycle

```
    ┌──────────────┐
    │   Scheduled  │
    └──────┬───────┘
           │
    ┌──────┴──────────┐
    │                 │
    ▼                 ▼
┌─────────┐    ┌──────────┐
│Completed│    │ Cancelled│
└────┬────┘    └──────────┘
     │
     ▼
┌──────────┐
│ Billing  │
│Generated │
└──────────┘
```

## 7. Sequence Diagram - Patient Registration

```
Patient        Frontend         Backend         Database
   │               │              │                │
   │ Fill Form     │              │                │
   ├──────────────▶│              │                │
   │               │              │                │
   │               │ Validate     │                │
   │               │ Form Data    │                │
   │               │              │                │
   │               │ POST Request │                │
   │               ├─────────────▶│                │
   │               │              │                │
   │               │              │ Check Email   │
   │               │              ├───────────────▶│
   │               │              │                │
   │               │              │ Email Exists? │
   │               │              │◀───────────────┤
   │               │              │                │
   │               │              │ Save Patient  │
   │               │              ├───────────────▶│
   │               │              │                │
   │               │              │ Return ID     │
   │               │              │◀───────────────┤
   │               │              │                │
   │               │ Success Resp │                │
   │               │◀─────────────┤                │
   │               │              │                │
   │ Confirmation  │              │                │
   │◀──────────────┤              │                │
   │               │              │                │
```

---

**Last Updated:** June 1, 2026  
**Diagrams Created By:** Mubarak Andarabi
