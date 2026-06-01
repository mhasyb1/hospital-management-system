# Installation & Setup Guide

## Prerequisites

Before installing the Hospital Management System, ensure you have the following installed:

### Required Software

1. **Node.js** (v14 or higher)
   - Download: https://nodejs.org/
   - Verify: `node --version`

2. **npm** (v6 or higher)
   - Usually comes with Node.js
   - Verify: `npm --version`

3. **MongoDB** (v4.0 or higher)
   - Download: https://www.mongodb.com/try/download/community
   - Verify: `mongod --version`

4. **Git**
   - Download: https://git-scm.com/
   - Verify: `git --version`

### System Requirements

- **OS**: Windows, macOS, or Linux
- **RAM**: Minimum 4GB (8GB recommended)
- **Storage**: 500MB free space
- **Browser**: Chrome, Firefox, Safari, or Edge (latest versions)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/mhasyb1/hospital-management-system.git
cd hospital-management-system
```

### 2. Install Dependencies

#### Backend Setup
```bash
cd backend
npm install
```

#### Frontend Setup
```bash
cd ../frontend
npm install
```

### 3. Configure Environment Variables

#### Create `.env` file in backend directory

```bash
# Database Configuration
MONGODB_URI=mongodb://localhost:27017/hospital-ms
DB_NAME=hospital-ms

# Server Configuration
PORT=5000
NODE_ENV=development

# JWT Configuration
JWT_SECRET=your-secret-key-here
JWT_EXPIRY=7d

# Email Configuration
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your-email@gmail.com
EMAIL_PASSWORD=your-app-password

# Frontend URL
FRONTEND_URL=http://localhost:3000

# Log Level
LOG_LEVEL=info
```

#### Create `.env` file in frontend directory

```bash
# Server URL
REACT_APP_API_URL=http://localhost:5000/api
NODE_ENV=development
```

### 4. Start MongoDB

```bash
# On Windows
mongod

# On macOS/Linux
mongod --dbpath /usr/local/var/mongodb
```

### 5. Start Backend Server

```bash
cd backend
npm start
```

Expected output:
```
Server running on port 5000
MongoDB connected
```

### 6. Start Frontend Server

Open a new terminal:

```bash
cd frontend
npm start
```

The application will automatically open at `http://localhost:3000`

## Verification

### Backend Health Check

```bash
curl http://localhost:5000/api/health
```

Expected response:
```json
{
  "status": "OK",
  "timestamp": "2026-06-01T10:00:00Z"
}
```

### Frontend Access

Open browser and navigate to:
- **Frontend**: http://localhost:3000
- **API Documentation**: http://localhost:5000/api/docs

## Project Structure

```
hospital-management-system/
├── backend/
│   ├── models/          # Database models
│   ├── controllers/     # Request handlers
│   ├── routes/          # API routes
│   ├── middleware/      # Custom middleware
│   ├── services/        # Business logic
│   ├── config/          # Configuration files
│   ├── .env             # Environment variables
│   └── server.js        # Entry point
├── frontend/
│   ├── public/          # Static files
│   ├── src/
│   │   ├── components/  # React components
│   │   ├── pages/       # Page components
│   │   ├── services/    # API services
│   │   ├── styles/      # CSS files
│   │   └── App.js       # Main app component
│   └── package.json
├── docs/                # Documentation files
├── screenshots/         # Project screenshots
├── README.md
└── package.json
```

## Available Scripts

### Backend

```bash
# Start development server with hot reload
npm run dev

# Start production server
npm start

# Run tests
npm test

# Run linter
npm run lint

# Fix linting issues
npm run lint:fix

# Generate API documentation
npm run docs
```

### Frontend

```bash
# Start development server
npm start

# Build for production
npm run build

# Run tests
npm test

# Run linter
npm run lint

# Preview production build
npm run serve
```

## Troubleshooting

### MongoDB Connection Error

**Error:** `MongoError: connect ECONNREFUSED 127.0.0.1:27017`

**Solution:**
```bash
# Make sure MongoDB is running
mongod

# Or use MongoDB Atlas cloud database
# Update MONGODB_URI in .env to your Atlas connection string
```

### Port Already in Use

**Error:** `EADDRINUSE: address already in use :::5000`

**Solution:**
```bash
# Find process using port 5000
netstat -ano | findstr :5000

# Kill the process
taskkill /PID <PID> /F

# Or use different port in .env
PORT=5001
```

### npm Install Issues

**Error:** `npm ERR! code ERESOLVE`

**Solution:**
```bash
# Clear npm cache
npm cache clean --force

# Install with legacy dependencies flag
npm install --legacy-peer-deps
```

### Module Not Found

**Error:** `Cannot find module 'express'`

**Solution:**
```bash
# Reinstall dependencies
rm -rf node_modules
npm install
```

## Initial Data Setup

### Create Admin User

```bash
cd backend
node scripts/create-admin.js
```

**Default Admin Credentials:**
- Email: admin@hospital.com
- Password: Admin@123

### Seed Sample Data

```bash
node scripts/seed-data.js
```

This will create:
- 10 sample patients
- 5 sample doctors
- 20 sample appointments

## Development Workflow

### 1. Create Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 2. Make Changes

Edit files as needed for your feature.

### 3. Test Your Changes

```bash
npm test
```

### 4. Commit Changes

```bash
git add .
git commit -m "[Feature] Add new feature description"
```

### 5. Push to Repository

```bash
git push origin feature/your-feature-name
```

### 6. Create Pull Request

Go to GitHub and create a PR from your feature branch to main.

## Deployment

### Deploy to Production

```bash
# Build frontend
cd frontend
npm run build

# Deploy to server (specific instructions in DEPLOYMENT.md)
```

## Additional Resources

- [API Documentation](./docs/API.md)
- [Database Schema](./docs/DATABASE.md)
- [Contributing Guidelines](./CONTRIBUTING.md)
- [Testing Guide](./TESTING.md)

## Support

For issues or questions:
1. Check [GitHub Issues](https://github.com/mhasyb1/hospital-management-system/issues)
2. Read project documentation
3. Contact project maintainers

---

**Last Updated:** June 1, 2026  
**Maintained By:** Mubarak Andarabi
