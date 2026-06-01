# Deployment Guide

## Deployment Strategy

This guide covers deploying the Hospital Management System to production environments.

## Pre-Deployment Checklist

- [ ] All tests passing (npm test)
- [ ] Code review completed
- [ ] Documentation updated
- [ ] Environment variables configured
- [ ] Database backups created
- [ ] Security audit completed
- [ ] Performance testing passed

## Deployment Environments

### Development Environment
- **URL:** http://localhost:3000
- **Database:** Local MongoDB
- **Purpose:** Development and testing
- **Auto-deploy:** From develop branch

### Staging Environment
- **URL:** https://staging-hms.example.com
- **Database:** Staging MongoDB
- **Purpose:** Pre-production testing
- **Auto-deploy:** From staging branch

### Production Environment
- **URL:** https://hms.example.com
- **Database:** Production MongoDB
- **Purpose:** Live system
- **Deploy:** Manual from main branch

## Deployment Platforms

### Option 1: Heroku

#### Prerequisites
- Heroku CLI installed
- Heroku account

#### Steps

```bash
# Install Heroku CLI
# npm install -g heroku

# Login to Heroku
heroku login

# Create Heroku app
heroku create hospital-management-system

# Add MongoDB Atlas URL
heroku config:set MONGODB_URI=<your-mongodb-url>

# Deploy from Git
git push heroku main

# View logs
heroku logs --tail
```

### Option 2: AWS (EC2)

#### Prerequisites
- AWS account
- EC2 instance running Ubuntu 20.04
- SSH access to instance

#### Steps

```bash
# Connect to instance
ssh -i your-key.pem ec2-user@your-instance.com

# Install Node.js
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt-get install -y nodejs

# Install MongoDB
sudo apt-get install -y mongodb

# Clone repository
git clone https://github.com/mhasyb1/hospital-management-system.git

# Install dependencies
cd hospital-management-system
npm install

# Create .env file
nano .env

# Start with PM2
sudo npm install -g pm2
pm2 start server.js
pm2 startup
pm2 save
```

### Option 3: DigitalOcean

#### Steps

```bash
# Create droplet (Ubuntu 20.04)

# Connect via SSH
ssh root@your-droplet-ip

# Update system
apt-get update && apt-get upgrade -y

# Install Node.js
curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
apt-get install -y nodejs

# Install Nginx
apt-get install -y nginx

# Configure Nginx as reverse proxy
# Copy nginx.conf configuration
```

## Environment Configuration

### Production .env Template

```bash
# Database
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/hospital-ms
DB_NAME=hospital-ms

# Server
PORT=3000
NODE_ENV=production

# Security
JWT_SECRET=your-long-random-secret-key-min-32-chars
JWT_EXPIRY=7d

# HTTPS
HTTPS=true
SSL_CERT_PATH=/path/to/cert.pem
SSL_KEY_PATH=/path/to/key.pem

# Email
EMAIL_HOST=smtp.sendgrid.net
EMAIL_PORT=587
EMAIL_USER=apikey
EMAIL_PASSWORD=your-sendgrid-key

# Frontend
FRONTEND_URL=https://hms.example.com

# Analytics
SENTRY_DSN=your-sentry-dsn
LOG_LEVEL=info

# Cache
REDIS_URL=redis://localhost:6379
SESSION_SECRET=your-session-secret
```

## Database Migration

### Backup MongoDB

```bash
# Local backup
mongodump --uri="mongodb://localhost:27017/hospital-ms" --out=./backup

# Cloud backup (MongoDB Atlas)
# Automatic backups enabled in cluster settings
```

### Restore from Backup

```bash
mongorestore --uri="mongodb://localhost:27017/hospital-ms" ./backup/hospital-ms
```

## SSL/HTTPS Setup

### Using Let's Encrypt (Recommended)

```bash
# Install Certbot
sudo apt-get install certbot python3-certbot-nginx

# Get certificate
sudo certbot certonly --nginx -d yourdomain.com

# Auto-renew setup
sudo certbot renew --dry-run

# Cron job for auto-renewal
0 12 * * * /usr/bin/certbot renew --quiet
```

### Update Nginx Configuration

```nginx
server {
    listen 443 ssl;
    server_name yourdomain.com;
    
    ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

## CI/CD Pipeline

### GitHub Actions Workflow

```yaml
name: Deploy to Production

on:
  push:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install
      - run: npm test
      - run: npm run build

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Deploy to Production
        run: |
          # Deploy commands here
          bash ./scripts/deploy.sh
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```

## Monitoring & Logging

### Application Monitoring

```bash
# Install PM2 Monitoring
pm2 install pm2-auto-pull
pm2 monitoring

# View logs
pm2 logs
pm2 logs --lines 100
```

### Error Tracking (Sentry)

```javascript
// In server.js
const Sentry = require("@sentry/node");

Sentry.init({ dsn: process.env.SENTRY_DSN });

app.use(Sentry.Handlers.requestHandler());
app.use(Sentry.Handlers.errorHandler());
```

### Application Performance Monitoring (APM)

- Use New Relic, DataDog, or similar service
- Monitor response times
- Track database queries
- Analyze CPU and memory usage

## Post-Deployment

### Verification Steps

1. **Health Check**
   ```bash
   curl https://hms.example.com/api/health
   ```

2. **Functionality Test**
   - Test patient registration
   - Test appointment booking
   - Test billing

3. **Performance Test**
   - Load testing
   - Response time validation

4. **Security Scan**
   - OWASP vulnerability scan
   - SSL certificate validation
   - Security headers check

### Rollback Procedure

If issues occur:

```bash
# For Heroku
heroku releases
heroku rollback v<number>

# For AWS/DigitalOcean
git revert <commit-hash>
npm start
```

## Scaling Considerations

### Horizontal Scaling

- Load balancer (Nginx, HAProxy)
- Multiple Node.js instances
- Session storage in Redis
- Database replication

### Vertical Scaling

- Upgrade server resources
- Optimize database queries
- Implement caching
- Enable compression

## Cost Optimization

| Service | Provider | Estimated Cost |
|---------|----------|-----------------|
| Hosting | DigitalOcean | $5-20/month |
| Database | MongoDB Atlas | $57-700+/month |
| Email | SendGrid | $10-50/month |
| SSL | Let's Encrypt | Free |
| **Total** | | **$72-770+/month** |

## Disaster Recovery

### Backup Strategy

- Daily automated backups
- Weekly full database backups
- Monthly backup verification
- Off-site backup storage

### Recovery Plan

- RTO (Recovery Time Objective): 1 hour
- RPO (Recovery Point Objective): 1 hour
- Documented recovery procedures
- Regular recovery testing

---

**Last Updated:** June 1, 2026  
**Maintained By:** Muhammad Haseeb
