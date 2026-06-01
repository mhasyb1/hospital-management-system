# Testing Plan

## Testing Strategy

This document outlines the comprehensive testing strategy for the Hospital Management System.

## Test Levels

### 1. Unit Testing

**Objective:** Test individual components in isolation

**Tools:**
- Jest (JavaScript testing framework)
- Mocha (Test runner)
- Chai (Assertion library)

**Coverage Target:** 80% code coverage

**Test Cases:**

#### Patient Model Tests
```javascript
describe('Patient Model', () => {
  - Test patient creation with valid data
  - Test validation of email format
  - Test phone number validation
  - Test date of birth validation
  - Test duplicate patient prevention
  - Test patient update
  - Test patient deletion
});
```

#### Doctor Model Tests
```javascript
describe('Doctor Model', () => {
  - Test doctor creation
  - Test specialization validation
  - Test license number validation
  - Test availability schedule
  - Test doctor search by specialization
});
```

#### Authentication Tests
```javascript
describe('Authentication Service', () => {
  - Test user login with valid credentials
  - Test login with invalid credentials
  - Test password hashing
  - Test JWT token generation
  - Test token verification
  - Test logout functionality
});
```

### 2. Integration Testing

**Objective:** Test multiple components working together

**Scope:**
- API endpoints with database
- Authentication with protected routes
- Appointment booking workflow
- Billing calculation

**Test Scenarios:**

#### Patient Registration to Appointment Flow
```
1. Register patient
2. Doctor searches available
3. Book appointment
4. Verify appointment in database
5. Send confirmation email
6. Update patient appointment list
```

#### Billing Integration
```
1. Complete appointment
2. Generate bill
3. Apply discounts/insurance
4. Calculate total
5. Record payment
6. Update billing history
```

### 3. System Testing

**Objective:** Test complete system functionality

**Test Scenarios:**
- Full patient journey (registration to billing)
- Multiple concurrent appointments
- Emergency override scenarios
- System recovery procedures
- Load and stress testing

**Performance Benchmarks:**
- Patient registration: < 2 seconds
- Appointment booking: < 1 second
- Report generation: < 5 seconds
- Database query: < 500ms

### 4. User Acceptance Testing (UAT)

**Objective:** Verify system meets business requirements

**Test Users:**
- Hospital administrators
- Doctors
- Patients
- Billing staff

**UAT Scenarios:**
1. Patient can register and view profile
2. Doctor can manage schedule
3. Patient can book appointment
4. System generates accurate bills
5. Admin can generate reports

## Test Execution Plan

### Phase 1: Unit Testing (Week 5-7)
- Develop unit tests alongside code
- Target 80% code coverage
- Run tests with every commit

### Phase 2: Integration Testing (Week 8-9)
- Test API endpoints
- Test database operations
- Test external services (email, payments)

### Phase 3: System Testing (Week 10)
- End-to-end testing
- Performance testing
- Security testing

### Phase 4: UAT (Week 11)
- User acceptance testing
- Feedback collection
- Bug fixing

## Test Cases by Module

### Patient Management

| Test Case | Input | Expected Output | Status |
|-----------|-------|-----------------|--------|
| Register new patient | Valid patient data | Patient created, confirmation sent | Pending |
| Validate email | Invalid email | Error message | Pending |
| Update patient | Updated data | Data saved | Pending |
| Search patient | Patient ID | Patient details retrieved | Pending |
| Delete patient | Patient ID | Patient deleted | Pending |

### Doctor Management

| Test Case | Input | Expected Output | Status |
|-----------|-------|-----------------|--------|
| Register doctor | Doctor details | Doctor created | Pending |
| Set availability | Schedule data | Schedule saved | Pending |
| Search by specialty | Specialty type | List of doctors | Pending |
| Update profile | New data | Profile updated | Pending |

### Appointment System

| Test Case | Input | Expected Output | Status |
|-----------|-------|-----------------|--------|
| Book appointment | Patient, Doctor, Date | Appointment created | Pending |
| Check availability | Doctor, Date | Available slots | Pending |
| Confirm appointment | Appointment ID | Confirmation sent | Pending |
| Cancel appointment | Appointment ID | Appointment cancelled | Pending |
| Reschedule | New date/time | Appointment updated | Pending |

### Billing System

| Test Case | Input | Expected Output | Status |
|-----------|-------|-----------------|--------|
| Generate bill | Appointment ID | Bill created | Pending |
| Apply discount | Discount code | Discount applied | Pending |
| Process payment | Payment details | Payment recorded | Pending |
| Generate invoice | Bill ID | Invoice PDF | Pending |

## Bug Severity Levels

| Severity | Description | Resolution Time | Example |
|----------|-------------|-----------------|---------|
| **Critical** | System crash, data loss | 24 hours | Login completely broken |
| **Major** | Feature not working | 72 hours | Appointments not saving |
| **Minor** | UI issue, typo | 1 week | Button misalignment |
| **Trivial** | Cosmetic issue | 2 weeks | Color inconsistency |

## Test Data

### Sample Patient Data
```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "phone": "+1234567890",
  "dateOfBirth": "1990-01-15",
  "gender": "Male",
  "address": "123 Main St, City"
}
```

### Sample Doctor Data
```json
{
  "firstName": "Dr. Jane",
  "lastName": "Smith",
  "specialization": "Cardiology",
  "licenseNumber": "MED123456",
  "experience": 10,
  "availability": "Mon-Fri 9AM-5PM"
}
```

## Testing Tools

### Backend Testing
- Jest
- Mocha
- Chai
- Supertest (API testing)

### Frontend Testing
- Jest
- React Testing Library
- Selenium (E2E)
- Cypress (E2E)

### Performance Testing
- Apache JMeter
- LoadRunner
- k6

### Security Testing
- OWASP ZAP
- Burp Suite
- npm audit

## Continuous Integration

### GitHub Actions Workflow
```yaml
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
      - run: npm install
      - run: npm test
      - run: npm run coverage
```

## Test Reporting

### Test Report Template
```
Test Summary Report
─────────────────────────────────────
Total Tests: 150
Passed: 145
Failed: 3
Skipped: 2
Pass Rate: 96.7%

Failed Tests:
1. Patient registration with duplicate email
2. Appointment booking past availability
3. Bill generation with invalid appointment

Recommendations:
- Fix email validation logic
- Improve date validation
- Update bill generation service
```

## Success Criteria

- ✓ 80% code coverage
- ✓ All critical bugs fixed
- ✓ 95% test pass rate
- ✓ Performance benchmarks met
- ✓ Zero security vulnerabilities
- ✓ UAT approved by all user groups

---

**Document Created:** June 1, 2026  
**Maintained By:** Mubarak Andarabi
