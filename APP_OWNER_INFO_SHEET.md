# Application Owner Information Sheet
**Last Updated:** 2025-12-31 06:26:06 (UTC)  
**Repository:** glory2godconstr2025-lab/verbose-spoon  
**Owner/Maintainer:** glory2godconstr2025-lab

---

## Table of Contents
1. [Quick Reference](#quick-reference)
2. [Access & Authentication](#access--authentication)
3. [Repository Structure](#repository-structure)
4. [Code Organization](#code-organization)
5. [Deployment Information](#deployment-information)
6. [Credentials & Secrets](#credentials--secrets)
7. [Monitoring & Logs](#monitoring--logs)
8. [Common Tasks & Procedures](#common-tasks--procedures)
9. [Emergency Contacts & Support](#emergency-contacts--support)

---

## Quick Reference

| Item | Description |
|------|-------------|
| **Repository Name** | verbose-spoon |
| **Repository Owner** | glory2godconstr2025-lab |
| **Repository URL** | https://github.com/glory2godconstr2025-lab/verbose-spoon |
| **Primary Branch** | main |
| **Current Date** | 2025-12-31 |
| **Documentation Date** | 2025-12-31 06:26:06 (UTC) |

---

## Access & Authentication

### GitHub Repository Access
- **Repository:** https://github.com/glory2godconstr2025-lab/verbose-spoon
- **Owner Account:** glory2godconstr2025-lab
- **Access Level:** Full repository access with administrative privileges
- **SSH Key Setup:** Ensure SSH keys are configured for seamless Git operations
  - Generate keys: `ssh-keygen -t ed25519 -C "your-email@example.com"`
  - Add public key to GitHub Settings → SSH and GPG keys
  - Test connection: `ssh -T git@github.com`

### GitHub Credentials
- **Username:** glory2godconstr2025-lab
- **Authentication Method:** SSH or Personal Access Token (PAT)
- **PAT Scope Requirements:**
  - `repo` - Full control of private repositories
  - `workflow` - Update GitHub Actions workflows
  - `admin:repo_hook` - Manage repository webhooks
  - `read:org` - Read organization data

### Required Access Levels
- **Repository**: Admin access (create branches, merge PRs, manage settings)
- **Deployments**: Access to deployment platforms/environments
- **Secrets Management**: Access to configure GitHub Secrets

---

## Repository Structure

```
verbose-spoon/
├── README.md                          # Project overview and documentation
├── APP_OWNER_INFO_SHEET.md           # This file - Owner management guide
├── .github/
│   ├── workflows/                     # GitHub Actions CI/CD pipelines
│   │   ├── deploy.yml                # Deployment workflow
│   │   ├── test.yml                  # Testing workflow
│   │   └── lint.yml                  # Code quality checks
│   └── PULL_REQUEST_TEMPLATE.md       # PR template for contributors
├── src/                               # Source code directory
│   ├── index.js                       # Application entry point
│   ├── config/                        # Configuration files
│   │   ├── env.js                    # Environment configuration
│   │   ├── database.js               # Database configuration
│   │   └── server.js                 # Server settings
│   ├── routes/                        # API routes
│   │   ├── auth.js                   # Authentication routes
│   │   ├── users.js                  # User management routes
│   │   └── api.js                    # General API routes
│   ├── controllers/                   # Business logic
│   ├── models/                        # Data models
│   ├── middleware/                    # Express middleware
│   └── utils/                         # Utility functions
├── tests/                             # Test suite
│   ├── unit/                          # Unit tests
│   └── integration/                   # Integration tests
├── docs/                              # Documentation
│   ├── API.md                         # API documentation
│   ├── ARCHITECTURE.md                # System architecture
│   └── SETUP.md                       # Setup instructions
├── config/                            # Configuration files
│   ├── .env.example                   # Example environment variables
│   ├── .env.production                # Production environment (NOT in repo)
│   └── .env.development               # Development environment (NOT in repo)
├── scripts/                           # Utility scripts
│   ├── deploy.sh                      # Deployment script
│   ├── setup.sh                       # Setup script
│   └── backup.sh                      # Backup script
├── package.json                       # Node.js dependencies and scripts
├── package-lock.json                  # Locked dependency versions
├── .gitignore                         # Files to exclude from Git
├── .env.example                       # Template for environment variables
├── LICENSE                            # Project license
└── CHANGELOG.md                       # Version history and changes

```

---

## Code Organization

### Key Files & Their Purposes

#### Entry Point
- **src/index.js** - Main application entry point
  - Initializes server
  - Loads environment configuration
  - Sets up middleware and routes
  - Starts listening on configured port

#### Configuration
- **src/config/env.js** - Environment-specific configuration
  - Loads environment variables
  - Validates required variables
  - Exports configuration object
- **src/config/database.js** - Database connection setup
  - Connection string management
  - Connection pooling
  - Error handling
- **src/config/server.js** - Server configuration
  - Port settings
  - CORS configuration
  - Request timeout settings

#### Routes & Endpoints
- **src/routes/auth.js** - Authentication endpoints
  - POST /auth/login
  - POST /auth/register
  - POST /auth/logout
  - POST /auth/refresh-token
- **src/routes/users.js** - User management
  - GET /users
  - GET /users/:id
  - POST /users
  - PUT /users/:id
  - DELETE /users/:id
- **src/routes/api.js** - General API endpoints
  - Application-specific endpoints

#### Middleware
- **src/middleware/** - Express middleware
  - Authentication verification
  - Error handling
  - Request validation
  - Logging
  - Rate limiting

#### Models & Controllers
- **src/models/** - Data schemas and ORM models
- **src/controllers/** - Business logic implementation

### Code Standards
- **Language:** JavaScript (Node.js)
- **Framework:** Express.js
- **Linting:** ESLint (configuration in .eslintrc)
- **Code Style:** Prettier
- **Testing Framework:** Jest or Mocha
- **Naming Conventions:**
  - camelCase for variables and functions
  - PascalCase for classes and models
  - UPPER_SNAKE_CASE for constants

---

## Deployment Information

### Deployment Environments

#### Development
- **URL:** http://localhost:3000
- **Database:** Local MongoDB or development database
- **Environment File:** `.env.development`
- **Commands:**
  ```bash
  npm install
  npm run dev
  ```

#### Staging
- **URL:** https://staging.example.com
- **Database:** Staging database instance
- **Deployment:** Automated via GitHub Actions on staging branch
- **Commands:**
  ```bash
  npm install
  npm run build
  npm start
  ```

#### Production
- **URL:** https://example.com
- **Database:** Production database instance
- **Deployment:** Manual or automated via GitHub Actions on main branch
- **Commands:**
  ```bash
  npm install
  npm run build
  npm start
  ```

### Deployment Process

#### Automatic Deployment (CI/CD)
1. **Trigger:** Push to main branch or merge PR
2. **Pipeline Steps:**
   - Code checkout
   - Install dependencies
   - Run linting
   - Run tests
   - Build application
   - Deploy to production
3. **Pipeline File:** `.github/workflows/deploy.yml`
4. **Status:** Check GitHub Actions tab for deployment status

#### Manual Deployment
1. SSH into production server
2. Navigate to application directory
3. Run: `git pull origin main`
4. Run: `npm install`
5. Run: `npm run build`
6. Restart service: `systemctl restart app-service` or `pm2 restart app`

### Deployment Checklist
- [ ] All tests passing
- [ ] Code review approved
- [ ] Environment variables configured
- [ ] Database migrations completed
- [ ] Backup created
- [ ] Monitoring alerts configured
- [ ] Rollback plan documented

### Rollback Procedure
1. Identify problematic commit/version
2. Revert: `git revert <commit-hash>` or `git checkout <stable-commit>`
3. Push to main: `git push origin main`
4. Monitor logs and health checks
5. Notify team of rollback

---

## Credentials & Secrets

### Environment Variables

#### Required Variables (Development)
```
NODE_ENV=development
PORT=3000
DATABASE_URL=mongodb://localhost:27017/verbose-spoon
JWT_SECRET=your-secret-key
API_KEY=your-api-key
LOG_LEVEL=debug
```

#### Required Variables (Production)
```
NODE_ENV=production
PORT=3000
DATABASE_URL=<production-mongodb-url>
JWT_SECRET=<secure-random-secret>
API_KEY=<production-api-key>
LOG_LEVEL=info
TLS_CERT_PATH=/etc/ssl/certs/cert.pem
TLS_KEY_PATH=/etc/ssl/private/key.pem
```

### Secret Management
- **Storage:** GitHub Secrets (Settings → Secrets and variables → Actions)
- **Database Credentials:** Never commit to repository
- **API Keys:** Store in GitHub Secrets or environment variables
- **SSL Certificates:** Store securely, reference via environment variables
- **JWT Secret:** Use strong, random string (32+ characters)

### Third-Party Integrations
Document any external services and their credentials:
- **Email Service:** (e.g., SendGrid, AWS SES)
- **Payment Gateway:** (e.g., Stripe, PayPal)
- **Cloud Storage:** (e.g., AWS S3, Google Cloud Storage)
- **Monitoring:** (e.g., Datadog, New Relic)

---

## Monitoring & Logs

### Application Logs
- **Location:** Application output or log files (configure path in .env)
- **Log Level:** Set via LOG_LEVEL environment variable
- **Rotation:** Implement log rotation to manage disk space
- **Retention:** Keep logs for at least 30 days

### Log Locations
```
/var/log/app/application.log          # Main application log
/var/log/app/error.log                # Error log
/var/log/app/access.log               # HTTP access log
```

### Monitoring Alerts
- **Health Check Endpoint:** GET /health
- **Uptime Monitoring:** Configure monitoring service
- **Error Tracking:** Set up error reporting (e.g., Sentry)
- **Performance Metrics:** Monitor CPU, memory, response times

### Health Check
```bash
curl -X GET http://localhost:3000/health
# Expected response: { "status": "ok", "timestamp": "..." }
```

### Common Issues & Solutions

#### Application won't start
1. Check logs: `tail -f /var/log/app/application.log`
2. Verify environment variables: `env | grep NODE_ENV`
3. Check port availability: `netstat -tulpn | grep 3000`
4. Restart service: `systemctl restart app-service`

#### Database connection issues
1. Verify DATABASE_URL is correct
2. Test connection: `mongosh <DATABASE_URL>`
3. Check database server status
4. Review credentials and permissions

#### High CPU/Memory usage
1. Check running processes: `ps aux | grep node`
2. Monitor real-time usage: `top`
3. Review application logs for errors
4. Implement rate limiting if under attack

---

## Common Tasks & Procedures

### Viewing Logs
```bash
# Real-time logs
tail -f /var/log/app/application.log

# Last 100 lines
tail -100 /var/log/app/application.log

# Search logs
grep "ERROR" /var/log/app/application.log

# Time-based search
grep "2025-12-31" /var/log/app/application.log
```

### Starting/Stopping Application
```bash
# Using systemctl
systemctl start app-service
systemctl stop app-service
systemctl restart app-service
systemctl status app-service

# Using PM2
pm2 start src/index.js --name app
pm2 stop app
pm2 restart app
pm2 logs app
```

### Database Management

#### Backup Database
```bash
# MongoDB backup
mongodump --uri="<DATABASE_URL>" --out=/backups/mongodb_backup_$(date +%Y%m%d)

# Run backup script
bash scripts/backup.sh
```

#### Restore Database
```bash
# MongoDB restore
mongorestore --uri="<DATABASE_URL>" /backups/mongodb_backup_YYYYMMDD
```

#### Database Migrations
```bash
# Run migrations (configure based on your migration tool)
npm run migrate:up

# Rollback migrations
npm run migrate:down
```

### Creating a Release
```bash
# Create version tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tag to remote
git push origin v1.0.0

# Create release via GitHub CLI
gh release create v1.0.0 --title "Version 1.0.0" --notes "Release notes here"
```

### Emergency Restart
```bash
# Kill all Node processes
pkill -9 node

# Restart service
systemctl restart app-service

# Verify service is running
systemctl status app-service
```

---

## Emergency Contacts & Support

### Key Team Members
| Role | Name | Email | Phone |
|------|------|-------|-------|
| Repository Owner | glory2godconstr2025-lab | [email] | [phone] |
| DevOps Engineer | [Name] | [email] | [phone] |
| Database Administrator | [Name] | [email] | [phone] |
| On-Call Support | [Name] | [email] | [phone] |

### Critical Incident Response
1. **Identify Issue:** Check monitoring alerts, logs, and health endpoints
2. **Notify Team:** Contact on-call engineer and team lead
3. **Assess Impact:** Determine affected users/services
4. **Implement Fix:** Apply temporary fix or rollback
5. **Communicate:** Update status page and notify users
6. **Post-Mortem:** Document incident and implement preventive measures

### Support Resources
- **GitHub Issues:** https://github.com/glory2godconstr2025-lab/verbose-spoon/issues
- **GitHub Discussions:** https://github.com/glory2godconstr2025-lab/verbose-spoon/discussions
- **Documentation:** See /docs directory
- **API Docs:** See docs/API.md

### Escalation Path
1. **Level 1:** Check documentation and logs
2. **Level 2:** Contact DevOps engineer
3. **Level 3:** Contact team lead/manager
4. **Level 4:** Executive escalation if critical

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2025-12-31 | Initial creation of APP_OWNER_INFO_SHEET.md |

---

**Note:** This document should be updated regularly as the application evolves. Last reviewed: 2025-12-31 06:26:06 (UTC)
