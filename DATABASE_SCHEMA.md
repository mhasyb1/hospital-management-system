# Database Schema

## Overview

Hospital Management System uses MongoDB with Mongoose ODM.

## Collections

### 1. Patients Collection

```javascript
{
  _id: ObjectId,
  firstName: String,
  lastName: String,
  email: String (unique, indexed),
  phone: String,
  dateOfBirth: Date,
  gender: String (enum: ['Male', 'Female', 'Other']),
  address: String,
  city: String,
  state: String,
  zipCode: String,
  medicalHistory: [
    {
      condition: String,
      diagnosisDate: Date,
      treatment: String,
      status: String
    }
  ],
  allergies: [String],
  emergencyContact: {
    name: String,
    phone: String,
    relationship: String
  },
  insuranceInfo: {
    provider: String,
    policyNumber: String,
    expiryDate: Date
  },
  appointments: [ObjectId],
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes:**
- `email`: unique, sparse
- `phone`: indexed
- `createdAt`: indexed

---

### 2. Doctors Collection

```javascript
{
  _id: ObjectId,
  firstName: String,
  lastName: String,
  email: String (unique, indexed),
  phone: String,
  specialization: String (indexed),
  licenseNumber: String (unique),
  experience: Number,
  education: [
    {
      degree: String,
      institution: String,
      graduationYear: Number
    }
  ],
  schedule: {
    monday: {startTime: String, endTime: String, available: Boolean},
    tuesday: {startTime: String, endTime: String, available: Boolean},
    wednesday: {startTime: String, endTime: String, available: Boolean},
    thursday: {startTime: String, endTime: String, available: Boolean},
    friday: {startTime: String, endTime: String, available: Boolean},
    saturday: {startTime: String, endTime: String, available: Boolean},
    sunday: {startTime: String, endTime: String, available: Boolean}
  },
  offDays: [Date],
  consultationFee: Number,
  isVerified: Boolean,
  appointments: [ObjectId],
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes:**
- `email`: unique, sparse
- `specialization`: indexed
- `licenseNumber`: unique

---

### 3. Appointments Collection

```javascript
{
  _id: ObjectId,
  patientId: ObjectId (ref: Patient),
  doctorId: ObjectId (ref: Doctor),
  appointmentDate: Date (indexed),
  appointmentTime: String,
  reason: String,
  notes: String,
  status: String (enum: ['Scheduled', 'Completed', 'Cancelled', 'No-Show']),
  duration: Number,
  consultationMode: String (enum: ['In-Person', 'Video', 'Phone']),
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes:**
- `patientId`: indexed
- `doctorId`: indexed
- `appointmentDate`: indexed
- `status`: indexed

---

### 4. Billing Collection

```javascript
{
  _id: ObjectId,
  appointmentId: ObjectId (ref: Appointment),
  patientId: ObjectId (ref: Patient),
  doctorId: ObjectId (ref: Doctor),
  billDate: Date,
  billNumber: String (unique),
  services: [
    {
      description: String,
      quantity: Number,
      unitPrice: Number,
      amount: Number
    }
  ],
  subTotal: Number,
  discounts: {
    type: String,
    amount: Number
  },
  taxes: {
    type: String,
    rate: Number,
    amount: Number
  },
  total: Number,
  status: String (enum: ['Pending', 'Paid', 'Overdue', 'Cancelled']),
  paymentMethod: String,
  paymentDate: Date,
  notes: String,
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes:**
- `appointmentId`: indexed
- `patientId`: indexed
- `billNumber`: unique
- `billDate`: indexed
- `status`: indexed

---

### 5. Users Collection

```javascript
{
  _id: ObjectId,
  firstName: String,
  lastName: String,
  email: String (unique, indexed),
  password: String (hashed),
  role: String (enum: ['Admin', 'Doctor', 'Patient', 'Staff']),
  isActive: Boolean,
  lastLogin: Date,
  lastPasswordChange: Date,
  passwordResetToken: String,
  passwordResetExpires: Date,
  twoFactorEnabled: Boolean,
  createdAt: Date,
  updatedAt: Date
}
```

**Indexes:**
- `email`: unique
- `role`: indexed

---

### 6. Admin Logs Collection

```javascript
{
  _id: ObjectId,
  userId: ObjectId (ref: User),
  action: String,
  targetModel: String,
  targetId: ObjectId,
  changes: {
    before: Object,
    after: Object
  },
  ipAddress: String,
  userAgent: String,
  status: String (enum: ['Success', 'Failed']),
  timestamp: Date
}
```

**Indexes:**
- `userId`: indexed
- `timestamp`: indexed

---

## Relationships Diagram

```
Patients (1) ──→ (N) Appointments ←── (1) Doctors
    │                      │
    │                      └───→ Billing
    │
    └─────────────────→ Users
                          
Users ────→ Admin Logs
```

## Database Connection

```javascript
// MongoDB Connection String
mongodb+srv://user:password@cluster.mongodb.net/hospital-ms

// Mongoose Connection
mongoose.connect(MONGODB_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

## Query Examples

### Get All Appointments for a Patient

```javascript
Appointment.find({ patientId: patientId })
  .populate('doctorId')
  .sort({ appointmentDate: -1 });
```

### Get Available Doctors

```javascript
Doctor.find({
  specialization: 'Cardiology',
  'schedule.monday.available': true
});
```

### Get Unpaid Bills

```javascript
Billing.find({ status: 'Pending' })
  .populate('patientId')
  .sort({ billDate: -1 });
```

### Generate Monthly Revenue Report

```javascript
Billing.aggregate([
  {
    $match: {
      billDate: {
        $gte: new Date('2026-06-01'),
        $lt: new Date('2026-07-01')
      },
      status: 'Paid'
    }
  },
  {
    $group: {
      _id: { $dateToString: { format: '%Y-%m-%d', date: '$billDate' } },
      totalRevenue: { $sum: '$total' },
      billCount: { $sum: 1 }
    }
  },
  { $sort: { _id: 1 } }
]);
```

## Backup Strategy

- Daily automated backups
- Weekly manual backups
- 30-day retention policy
- Test restore quarterly

---

**Last Updated:** June 1, 2026  
**Version:** 1.0
