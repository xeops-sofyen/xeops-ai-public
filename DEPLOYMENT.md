# 🚀 XeOps.ai - Deployment Guide

**Last Updated**: October 20, 2025
**Production Status**: ✅ Live on GCP Cloud Run
**Target Audience**: DevOps Engineers, Platform Engineers

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Environment Setup](#environment-setup)
3. [Deployment Process](#deployment-process)
4. [Service-Specific Deployment](#service-specific-deployment)
5. [Database Management](#database-management)
6. [Secrets Management](#secrets-management)
7. [Domain Configuration](#domain-configuration)
8. [Monitoring & Validation](#monitoring--validation)
9. [Rollback Procedures](#rollback-procedures)
10. [Troubleshooting](#troubleshooting)

---

## ✅ Prerequisites

### Required Tools

```bash
# Install Google Cloud SDK
curl https://sdk.cloud.google.com | bash
exec -l $SHELL

# Install gcloud components
gcloud components install beta
gcloud components update

# Verify installation
gcloud --version
```

### Required Access

- ✅ GCP Project Admin access (`xeops-ai`)
- ✅ Cloud Run Admin role
- ✅ Cloud SQL Admin role
- ✅ Secret Manager Admin role
- ✅ Cloud Build Editor role
- ✅ Service Account User role

### Verify Access

```bash
# Login to GCP
gcloud auth login

# Set project
gcloud config set project xeops-ai

# Verify permissions
gcloud projects get-iam-policy xeops-ai --flatten="bindings[].members" --filter="bindings.members:user:YOUR_EMAIL"
```

---

## 🔧 Environment Setup

### 1. Clone Repositories

```bash
# Main platform repository (private)
git clone https://github.com/sofyenmarzougui/xeops.git
cd xeops

# Public documentation (optional)
git clone https://github.com/xeops-sofyen/xeops-ai-public.git
```

### 2. Configure GCP

```bash
# Set default region
gcloud config set run/region europe-west1

# Enable required APIs
gcloud services enable run.googleapis.com
gcloud services enable cloudbuild.googleapis.com
gcloud services enable sqladmin.googleapis.com
gcloud services enable secretmanager.googleapis.com
gcloud services enable cloudresourcemanager.googleapis.com
```

### 3. Environment Variables

Create `.env.production` file:

```bash
# Project Configuration
GCP_PROJECT_ID=xeops-ai
GCP_REGION=europe-west1

# Service URLs (auto-generated after first deploy)
FRONTEND_URL=https://www.xeops.ai
API_GATEWAY_URL=https://xeops-api-gateway-97758009309.europe-west1.run.app
AUTH_SERVICE_URL=https://xeops-auth-service-97758009309.europe-west1.run.app
SCANNER_SERVICE_URL=https://xeops-scanner-97758009309.europe-west1.run.app

# Database
DATABASE_URL=postgresql://user:pass@/cloudsql/xeops-ai:europe-west1:xeops-db-prod/xeops

# Stripe (use test keys for staging)
STRIPE_PUBLIC_KEY=pk_live_xxxxx
STRIPE_SECRET_KEY=sk_live_xxxxx

# SMTP
SMTP_USER=noreply@xeops.ai
SMTP_PASSWORD=stored-in-secrets-manager
```

---

## 🚀 Deployment Process

### Production Deployment Workflow

```
1. Code changes → Git push to master
2. Run tests locally (npm test)
3. Build & test in staging (optional)
4. Deploy to production
5. Run smoke tests
6. Monitor for errors
7. Rollback if needed
```

### Pre-Deployment Checklist

- [ ] All tests passing (`npm test`)
- [ ] Code reviewed and approved
- [ ] Database migrations ready (if any)
- [ ] Secrets updated (if needed)
- [ ] Rollback plan prepared
- [ ] Monitoring dashboards ready
- [ ] Team notified of deployment

---

## 🎯 Service-Specific Deployment

### 1. Frontend (Next.js)

**Directory**: `/apps/landing-page`

**Build & Deploy**:
```bash
cd apps/landing-page

# Install dependencies
npm install

# Build locally to verify
npm run build

# Deploy to Cloud Run
gcloud run deploy xeops-frontend \
  --source . \
  --platform managed \
  --region europe-west1 \
  --allow-unauthenticated \
  --set-env-vars \
    NODE_ENV=production,\
    NEXT_PUBLIC_API_URL=https://xeops-api-gateway-97758009309.europe-west1.run.app,\
    NEXT_PUBLIC_APP_NAME=XeOps,\
    NEXT_PUBLIC_APP_URL=https://www.xeops.ai,\
    NEXT_PUBLIC_ENABLE_ANALYTICS=true,\
    NEXT_PUBLIC_ENABLE_CHAT=true \
  --memory 512Mi \
  --cpu 1 \
  --min-instances 0 \
  --max-instances 10 \
  --timeout 60 \
  --project xeops-ai
```

**Expected Output**:
```
✓ Building and deploying new service [xeops-frontend]
✓ Creating Container Repository...
✓ Uploading sources...
✓ Building container image...
✓ Deploying Container...
Service [xeops-frontend] revision [xeops-frontend-00004-xyz] has been deployed
Service URL: https://xeops-frontend-5jseu3edda-ew.a.run.app
```

**Validation**:
```bash
# Test homepage
curl -I https://www.xeops.ai

# Check load time
time curl -s https://www.xeops.ai > /dev/null

# Verify cache headers
curl -I https://www.xeops.ai | grep -i cache
```

---

### 2. API Gateway (Node.js + Express)

**Directory**: `/services/api-gateway`

**Build & Deploy**:
```bash
cd services/api-gateway

# Install dependencies
npm install

# Run tests
npm test

# Deploy
gcloud run deploy xeops-api-gateway \
  --source . \
  --platform managed \
  --region europe-west1 \
  --allow-unauthenticated \
  --set-env-vars \
    NODE_ENV=production,\
    AUTH_SERVICE_URL=https://xeops-auth-service-97758009309.europe-west1.run.app,\
    SCANNER_SERVICE_URL=https://xeops-scanner-97758009309.europe-west1.run.app \
  --memory 512Mi \
  --cpu 1 \
  --min-instances 0 \
  --max-instances 20 \
  --timeout 60 \
  --project xeops-ai
```

**Validation**:
```bash
# Health check
curl https://xeops-api-gateway-97758009309.europe-west1.run.app/health

# Expected response:
# {
#   "status": "healthy",
#   "service": "api-gateway",
#   "version": "2.0.0-consolidated"
# }
```

---

### 3. Authentication Service (Node.js + JWT)

**Directory**: `/services/auth-service`

**Build & Deploy**:
```bash
cd services/auth-service

# Install dependencies
npm install

# Run tests
npm test

# Deploy with secrets
gcloud run deploy xeops-auth-service \
  --source . \
  --platform managed \
  --region europe-west1 \
  --allow-unauthenticated \
  --set-secrets \
    DATABASE_URL=xeops-database-url:latest,\
    JWT_SECRET=xeops-jwt-secret:latest,\
    SMTP_PASSWORD=xeops-smtp-password:latest \
  --set-env-vars \
    NODE_ENV=production,\
    SMTP_USER=noreply@xeops.ai \
  --memory 512Mi \
  --cpu 1 \
  --min-instances 0 \
  --max-instances 10 \
  --timeout 60 \
  --project xeops-ai
```

**Validation**:
```bash
# Health check
curl https://xeops-auth-service-97758009309.europe-west1.run.app/health

# Expected response:
# {
#   "status": "ok",
#   "service": "authentication-service",
#   "version": "1.0.0"
# }

# Test signup (should return 201 or validation error)
curl -X POST https://xeops-auth-service-97758009309.europe-west1.run.app/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"TestPass123!"}'
```

---

### 4. Scanner Service (Python + FastAPI)

**Directory**: `/services/scanner-service`

**Build & Deploy**:
```bash
cd services/scanner-service

# Install dependencies
pip install -r requirements.txt

# Run tests
pytest

# Deploy
gcloud run deploy xeops-scanner \
  --source . \
  --platform managed \
  --region europe-west1 \
  --allow-unauthenticated \
  --set-secrets \
    DATABASE_URL=xeops-database-url:latest \
  --set-env-vars \
    NODE_ENV=production \
  --memory 1Gi \
  --cpu 2 \
  --timeout 900 \
  --min-instances 0 \
  --max-instances 5 \
  --project xeops-ai
```

**⚠️ Known Issue**:
The health endpoint currently returns 404. This needs to be fixed before production launch.

**Validation** (after fix):
```bash
# Health check (currently failing - TODO: fix)
curl https://xeops-scanner-97758009309.europe-west1.run.app/health

# Expected response (after fix):
# {
#   "status": "healthy",
#   "service": "scanner",
#   "version": "1.0.0"
# }
```

**Priority**: 🔴 P0 - Must fix before announcing production

---

## 🗄️ Database Management

### Cloud SQL Instance

**Instance ID**: `xeops-db-prod`
**Type**: PostgreSQL 15
**Region**: europe-west1

### Database Migrations

**Using Prisma**:
```bash
cd services/auth-service

# Generate migration
npx prisma migrate dev --name migration_name

# Apply to production
npx prisma migrate deploy

# Verify schema
npx prisma db pull
```

**Using Raw SQL**:
```bash
# Connect to Cloud SQL
gcloud sql connect xeops-db-prod --user=postgres --database=xeops

# Run migration
\i migrations/001_add_new_table.sql
```

### Backup & Restore

**Create Backup**:
```bash
gcloud sql backups create \
  --instance=xeops-db-prod \
  --project=xeops-ai
```

**Restore Backup**:
```bash
# List backups
gcloud sql backups list --instance=xeops-db-prod

# Restore
gcloud sql backups restore BACKUP_ID \
  --backup-instance=xeops-db-prod \
  --backup-project=xeops-ai
```

**Export to Storage**:
```bash
# Export to Cloud Storage
gcloud sql export sql xeops-db-prod \
  gs://xeops-backups/$(date +%Y%m%d)-backup.sql \
  --database=xeops
```

---

## 🔐 Secrets Management

### Creating Secrets

```bash
# Database URL
echo -n "postgresql://user:pass@/cloudsql/xeops-ai:europe-west1:xeops-db-prod/xeops" | \
  gcloud secrets create xeops-database-url \
    --data-file=- \
    --replication-policy=automatic

# JWT Secret
openssl rand -base64 32 | \
  gcloud secrets create xeops-jwt-secret \
    --data-file=- \
    --replication-policy=automatic

# SMTP Password
echo -n "your-smtp-password" | \
  gcloud secrets create xeops-smtp-password \
    --data-file=- \
    --replication-policy=automatic
```

### Updating Secrets

```bash
# Add new version
echo -n "new-secret-value" | \
  gcloud secrets versions add xeops-jwt-secret --data-file=-

# List versions
gcloud secrets versions list xeops-jwt-secret

# Disable old version
gcloud secrets versions disable VERSION_NUMBER --secret=xeops-jwt-secret
```

### Granting Access

```bash
# Grant Cloud Run service account access to secret
gcloud secrets add-iam-policy-binding xeops-database-url \
  --member="serviceAccount:SERVICE_ACCOUNT_EMAIL" \
  --role="roles/secretmanager.secretAccessor"
```

---

## 🌐 Domain Configuration

### Custom Domain Mapping

**Map www.xeops.ai to Frontend**:
```bash
# Create domain mapping
gcloud beta run domain-mappings create \
  --service xeops-frontend \
  --domain www.xeops.ai \
  --region europe-west1 \
  --project xeops-ai
```

**Map api.xeops.ai to API Gateway** (Future):
```bash
gcloud beta run domain-mappings create \
  --service xeops-api-gateway \
  --domain api.xeops.ai \
  --region europe-west1 \
  --project xeops-ai
```

### DNS Configuration

**Required DNS Records**:
```
Type: CNAME
Name: www
Value: ghs.googlehosted.com.
TTL: 3600

Type: A
Name: @
Value: [IP from domain mapping]
TTL: 3600
```

**Verify Mapping**:
```bash
# Check domain mapping status
gcloud beta run domain-mappings describe \
  --domain www.xeops.ai \
  --region europe-west1 \
  --project xeops-ai

# Test DNS resolution
dig www.xeops.ai +short
nslookup www.xeops.ai
```

**Current Status** (Oct 20, 2025):
- ✅ www.xeops.ai → Frontend (working)
- ⏳ api.xeops.ai → API Gateway (not configured yet)

---

## 📊 Monitoring & Validation

### Health Checks

**Post-Deployment Validation Script**:
```bash
#!/bin/bash

echo "🔍 XeOps Production Health Check"
echo "================================"

# Frontend
echo -n "Frontend (www.xeops.ai): "
if curl -s -o /dev/null -w "%{http_code}" https://www.xeops.ai | grep -q "200"; then
  echo "✅ OK"
else
  echo "❌ FAILED"
fi

# API Gateway
echo -n "API Gateway: "
if curl -s https://xeops-api-gateway-97758009309.europe-west1.run.app/health | grep -q "healthy"; then
  echo "✅ OK"
else
  echo "❌ FAILED"
fi

# Auth Service
echo -n "Auth Service: "
if curl -s https://xeops-auth-service-97758009309.europe-west1.run.app/health | grep -q "ok"; then
  echo "✅ OK"
else
  echo "❌ FAILED"
fi

# Scanner Service (expected to fail until P0 fix)
echo -n "Scanner Service: "
if curl -s https://xeops-scanner-97758009309.europe-west1.run.app/health | grep -q "healthy"; then
  echo "✅ OK"
else
  echo "⚠️  FAILED (known issue - P0)"
fi

echo "================================"
```

### Performance Monitoring

**Cloud Monitoring Dashboard**:
```bash
# View service metrics
gcloud run services describe xeops-frontend \
  --region europe-west1 \
  --format="value(status.url,status.latestReadyRevisionName)"

# View logs
gcloud logging read "resource.type=cloud_run_revision AND resource.labels.service_name=xeops-frontend" \
  --limit 50 \
  --format json
```

### E2E Tests

**Run Production E2E Tests**:
```bash
cd apps/landing-page

# Set production URL
export BASE_URL=https://www.xeops.ai

# Run critical P0 tests
npm run test:e2e -- --grep "P0"

# Check results
cat /tmp/p0-test-validation-final.log
```

---

## ⏮️ Rollback Procedures

### Rollback to Previous Revision

**List Revisions**:
```bash
gcloud run revisions list \
  --service xeops-frontend \
  --region europe-west1 \
  --limit 5
```

**Rollback**:
```bash
# Route 100% traffic to previous revision
gcloud run services update-traffic xeops-frontend \
  --to-revisions=PREVIOUS_REVISION=100 \
  --region europe-west1
```

**Emergency Rollback Script**:
```bash
#!/bin/bash

SERVICE=$1
REVISION=$2

if [ -z "$SERVICE" ] || [ -z "$REVISION" ]; then
  echo "Usage: ./rollback.sh <service-name> <revision-name>"
  exit 1
fi

echo "🔄 Rolling back $SERVICE to $REVISION..."

gcloud run services update-traffic $SERVICE \
  --to-revisions=$REVISION=100 \
  --region europe-west1 \
  --project xeops-ai

echo "✅ Rollback complete. Verify at:"
gcloud run services describe $SERVICE --region europe-west1 --format='value(status.url)'
```

### Database Rollback

**Restore from Backup**:
```bash
# List backups
gcloud sql backups list --instance=xeops-db-prod

# Restore (creates new instance)
gcloud sql backups restore BACKUP_ID \
  --backup-instance=xeops-db-prod \
  --backup-project=xeops-ai
```

⚠️ **Warning**: Database rollback is destructive. Always verify backup before restoring.

---

## 🐛 Troubleshooting

### Common Issues

#### Issue: "Service not found" error

**Solution**:
```bash
# Verify service exists
gcloud run services list --region europe-west1

# Verify project
gcloud config get-value project
```

#### Issue: "Permission denied" error

**Solution**:
```bash
# Check IAM roles
gcloud projects get-iam-policy xeops-ai

# Grant required role
gcloud projects add-iam-policy-binding xeops-ai \
  --member="user:YOUR_EMAIL" \
  --role="roles/run.admin"
```

#### Issue: Container build fails

**Solution**:
```bash
# Check Cloud Build logs
gcloud builds list --limit=5

# View specific build
gcloud builds log BUILD_ID
```

#### Issue: Service returns 503

**Solution**:
```bash
# Check service logs
gcloud logging read "resource.type=cloud_run_revision" \
  --limit 100 \
  --format json

# Check container health
gcloud run revisions describe REVISION_NAME --region europe-west1
```

#### Issue: Database connection fails

**Solution**:
```bash
# Verify Cloud SQL instance is running
gcloud sql instances describe xeops-db-prod

# Test connection from Cloud Shell
gcloud sql connect xeops-db-prod --user=postgres

# Check secrets are accessible
gcloud secrets versions access latest --secret=xeops-database-url
```

### Logs Access

**View Real-Time Logs**:
```bash
# Frontend logs
gcloud run services logs tail xeops-frontend --region europe-west1

# API Gateway logs
gcloud run services logs tail xeops-api-gateway --region europe-west1

# Filter by severity
gcloud logging read "resource.type=cloud_run_revision AND severity>=ERROR" --limit 50
```

**Download Logs**:
```bash
# Export logs to Cloud Storage
gcloud logging sinks create xeops-logs-export \
  gs://xeops-logs-bucket/ \
  --log-filter='resource.type="cloud_run_revision"'
```

---

## 📞 Support

**Deployment Issues**:
- DevOps Lead: sofyen.marzougui@xeops.ai
- Emergency: contact@xeops.ai

**GCP Support**:
- Console: https://console.cloud.google.com/run?project=xeops-ai
- Support: https://cloud.google.com/support

**Documentation**:
- [ARCHITECTURE.md](./ARCHITECTURE.md) - System architecture
- [API_GUIDE.md](./API_GUIDE.md) - API documentation
- [GETTING_STARTED.md](./GETTING_STARTED.md) - User guide

---

## 📋 Deployment Checklist

### Pre-Deployment
- [ ] All tests passing
- [ ] Code reviewed
- [ ] Database migrations prepared
- [ ] Secrets verified
- [ ] Rollback plan ready
- [ ] Team notified

### During Deployment
- [ ] Deploy each service sequentially
- [ ] Verify health checks pass
- [ ] Check logs for errors
- [ ] Run smoke tests
- [ ] Monitor metrics

### Post-Deployment
- [ ] All services responding
- [ ] E2E tests passing
- [ ] Performance within SLA
- [ ] No error spikes in logs
- [ ] Documentation updated
- [ ] Team notified of completion

---

**Document Version**: 1.0
**Last Updated**: October 20, 2025
**Next Review**: November 20, 2025
