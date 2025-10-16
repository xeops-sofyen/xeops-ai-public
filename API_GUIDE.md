# 🔌 XeOps.ai API Guide

Complete API reference for integrating XeOps.ai security scanning into your applications and CI/CD pipelines.

---

## 📋 Table of Contents

1. [Authentication](#authentication)
2. [Base URL](#base-url)
3. [Rate Limits](#rate-limits)
4. [Endpoints](#endpoints)
5. [Webhooks](#webhooks)
6. [Error Handling](#error-handling)
7. [Code Examples](#code-examples)
8. [CI/CD Integration](#cicd-integration)

---

## 🔐 Authentication

XeOps API uses Bearer token authentication.

### Getting Your API Key

1. Login to your [dashboard](https://xeops.ai/dashboard)
2. Go to **Profile > API Keys**
3. Click **"Generate New API Key"**
4. Copy and securely store your key

### Using Your API Key

Include your API key in the `Authorization` header:

```bash
Authorization: Bearer YOUR_API_KEY_HERE
```

**Example:**
```bash
curl -X GET https://api.xeops.ai/api/scans \
  -H "Authorization: Bearer xeops_live_1234567890abcdef"
```

---

## 🌐 Base URL

```
https://api.xeops.ai
```

All API requests must use HTTPS. HTTP requests will be redirected.

---

## ⏱️ Rate Limits

Rate limits vary by plan:

| Plan | Requests/Hour | Requests/Day | Concurrent Scans |
|------|---------------|--------------|-------------------|
| Free | 10 | 50 | 1 |
| Professional | 100 | 1,000 | 3 |
| Enterprise | Unlimited | Unlimited | Unlimited |

**Response Headers:**
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1634567890
```

**Rate Limit Exceeded (429):**
```json
{
  "error": "rate_limit_exceeded",
  "message": "API rate limit exceeded",
  "retry_after": 3600
}
```

---

## 📡 Endpoints

### Health Check

Check API status and connectivity.

```http
GET /health
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2025-10-16T10:00:00Z",
  "version": "1.0.0"
}
```

---

### Create Scan

Start a new security scan.

```http
POST /api/scan
```

**Headers:**
```
Authorization: Bearer YOUR_API_KEY
Content-Type: application/json
```

**Body:**
```json
{
  "target": "https://api.example.com",
  "scan_type": "standard",
  "description": "API security audit",
  "intensity": "normal",
  "authentication": {
    "type": "bearer",
    "token": "your-test-api-token"
  },
  "scope": {
    "include_subdomains": false,
    "max_endpoints": 100
  },
  "notifications": {
    "email": true,
    "webhook_url": "https://your-app.com/webhooks/xeops"
  }
}
```

**Parameters:**

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `target` | string | Yes | URL to scan (must start with https://) |
| `scan_type` | string | Yes | `quick`, `standard`, or `deep` |
| `description` | string | No | Human-readable scan description |
| `intensity` | string | No | `light`, `normal`, or `aggressive` (default: `normal`) |
| `authentication` | object | No | Auth credentials for protected endpoints |
| `scope` | object | No | Scan scope configuration |
| `notifications` | object | No | Notification preferences |

**Response (201 Created):**
```json
{
  "scan_id": "scan_abc123xyz",
  "status": "queued",
  "target": "https://api.example.com",
  "scan_type": "standard",
  "created_at": "2025-10-16T10:00:00Z",
  "estimated_completion": "2025-10-16T10:30:00Z",
  "dashboard_url": "https://xeops.ai/dashboard/scans/scan_abc123xyz"
}
```

---

### Get Scan Status

Retrieve the status of a running or completed scan.

```http
GET /api/scan/:scan_id
```

**Response:**
```json
{
  "scan_id": "scan_abc123xyz",
  "status": "running",
  "target": "https://api.example.com",
  "scan_type": "standard",
  "progress": 45,
  "started_at": "2025-10-16T10:00:00Z",
  "updated_at": "2025-10-16T10:15:00Z",
  "findings": {
    "critical": 0,
    "high": 2,
    "medium": 5,
    "low": 8,
    "info": 12
  }
}
```

**Status Values:**
- `queued` - Scan is waiting to start
- `running` - Scan is in progress
- `completed` - Scan finished successfully
- `failed` - Scan encountered an error
- `canceled` - Scan was canceled by user

---

### Get Scan Results

Retrieve detailed findings from a completed scan.

```http
GET /api/scan/:scan_id/results
```

**Query Parameters:**
- `severity` (optional): Filter by severity (`critical`, `high`, `medium`, `low`, `info`)
- `format` (optional): Response format (`json`, `pdf`, `html`, `csv`)

**Response:**
```json
{
  "scan_id": "scan_abc123xyz",
  "status": "completed",
  "target": "https://api.example.com",
  "started_at": "2025-10-16T10:00:00Z",
  "completed_at": "2025-10-16T10:30:00Z",
  "summary": {
    "total_findings": 27,
    "critical": 0,
    "high": 2,
    "medium": 5,
    "low": 8,
    "info": 12,
    "endpoints_tested": 43,
    "requests_sent": 287
  },
  "findings": [
    {
      "id": "vuln_def456",
      "severity": "high",
      "type": "SQL Injection",
      "cwe": "CWE-89",
      "cvss": 8.5,
      "title": "SQL Injection in /api/users endpoint",
      "description": "The /api/users endpoint is vulnerable to SQL injection...",
      "affected_component": {
        "url": "https://api.example.com/api/users",
        "method": "GET",
        "parameter": "id"
      },
      "proof_of_concept": {
        "request": "GET /api/users?id=1' OR '1'='1 HTTP/1.1",
        "response_indicator": "Returned all users instead of single user"
      },
      "impact": "An attacker could extract, modify, or delete database contents...",
      "remediation": {
        "summary": "Use parameterized queries",
        "steps": [
          "Replace string concatenation with prepared statements",
          "Use ORM with parameterized queries",
          "Implement input validation"
        ],
        "code_example": "// Use parameterized query\\nconst query = 'SELECT * FROM users WHERE id = ?';\\ndb.query(query, [userId]);"
      },
      "references": [
        "https://owasp.org/www-community/attacks/SQL_Injection",
        "https://cwe.mitre.org/data/definitions/89.html"
      ]
    }
  ]
}
```

---

### List Scans

Get a list of all your scans.

```http
GET /api/scans
```

**Query Parameters:**
- `status` (optional): Filter by status
- `limit` (optional): Number of results (default: 20, max: 100)
- `offset` (optional): Pagination offset

**Response:**
```json
{
  "scans": [
    {
      "scan_id": "scan_abc123",
      "target": "https://api.example.com",
      "status": "completed",
      "created_at": "2025-10-16T10:00:00Z",
      "findings_count": 27
    }
  ],
  "pagination": {
    "total": 150,
    "limit": 20,
    "offset": 0,
    "has_more": true
  }
}
```

---

### Cancel Scan

Stop a running scan.

```http
DELETE /api/scan/:scan_id
```

**Response (200 OK):**
```json
{
  "scan_id": "scan_abc123xyz",
  "status": "canceled",
  "message": "Scan canceled successfully"
}
```

---

## 🪝 Webhooks

Receive real-time notifications about scan events.

### Setup

1. Go to **Dashboard > Profile > Webhooks**
2. Add your webhook URL
3. Select events to receive
4. Save and copy the signing secret

### Webhook Events

**Available Events:**
- `scan.queued` - Scan added to queue
- `scan.started` - Scan execution started
- `scan.progress` - Scan progress update (every 10%)
- `scan.completed` - Scan finished successfully
- `scan.failed` - Scan encountered error
- `vulnerability.found` - New vulnerability detected

### Webhook Payload

```json
{
  "event": "scan.completed",
  "timestamp": "2025-10-16T10:30:00Z",
  "data": {
    "scan_id": "scan_abc123xyz",
    "target": "https://api.example.com",
    "status": "completed",
    "findings_count": 27,
    "critical_count": 0,
    "high_count": 2,
    "dashboard_url": "https://xeops.ai/dashboard/scans/scan_abc123xyz"
  }
}
```

### Webhook Signature Verification

Verify webhook authenticity using HMAC-SHA256:

```python
import hmac
import hashlib

def verify_webhook(payload, signature, secret):
    expected = hmac.new(
        secret.encode(),
        payload.encode(),
        hashlib.sha256
    ).hexdigest()
    return hmac.compare_digest(expected, signature)

# Usage
signature = request.headers.get('X-XeOps-Signature')
is_valid = verify_webhook(request.body, signature, webhook_secret)
```

---

## ❌ Error Handling

### Error Response Format

```json
{
  "error": "error_code",
  "message": "Human-readable error message",
  "details": {
    "field": "Specific error details"
  },
  "request_id": "req_abc123xyz"
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `invalid_request` | 400 | Malformed request body |
| `authentication_required` | 401 | Missing or invalid API key |
| `insufficient_permissions` | 403 | API key lacks required permissions |
| `resource_not_found` | 404 | Scan ID not found |
| `rate_limit_exceeded` | 429 | Too many requests |
| `server_error` | 500 | Internal server error |
| `service_unavailable` | 503 | Service temporarily unavailable |

---

## 💻 Code Examples

### Python

```python
import requests

API_KEY = "xeops_live_your_api_key"
BASE_URL = "https://api.xeops.ai"

headers = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}

# Create scan
response = requests.post(
    f"{BASE_URL}/api/scan",
    headers=headers,
    json={
        "target": "https://api.example.com",
        "scan_type": "standard",
        "description": "Weekly security audit"
    }
)

scan = response.json()
scan_id = scan["scan_id"]
print(f"Scan created: {scan_id}")

# Check status
import time

while True:
    response = requests.get(
        f"{BASE_URL}/api/scan/{scan_id}",
        headers=headers
    )
    status = response.json()

    if status["status"] == "completed":
        print(f"Scan completed! Found {status['findings']['total']} vulnerabilities")
        break
    elif status["status"] == "failed":
        print("Scan failed!")
        break

    print(f"Progress: {status['progress']}%")
    time.sleep(30)

# Get results
response = requests.get(
    f"{BASE_URL}/api/scan/{scan_id}/results",
    headers=headers
)

results = response.json()
for finding in results["findings"]:
    if finding["severity"] in ["critical", "high"]:
        print(f"⚠️  {finding['severity'].upper()}: {finding['title']}")
```

### JavaScript/Node.js

```javascript
const axios = require('axios');

const API_KEY = 'xeops_live_your_api_key';
const BASE_URL = 'https://api.xeops.ai';

const client = axios.create({
  baseURL: BASE_URL,
  headers: {
    'Authorization': `Bearer ${API_KEY}`,
    'Content-Type': 'application/json'
  }
});

// Create and monitor scan
async function runScan() {
  try {
    // Create scan
    const { data: scan } = await client.post('/api/scan', {
      target: 'https://api.example.com',
      scan_type: 'standard',
      description: 'Weekly security audit'
    });

    console.log(`Scan created: ${scan.scan_id}`);

    // Poll for completion
    let status;
    do {
      await new Promise(resolve => setTimeout(resolve, 30000)); // Wait 30s

      const { data } = await client.get(`/api/scan/${scan.scan_id}`);
      status = data;

      console.log(`Progress: ${status.progress}%`);
    } while (status.status === 'running');

    if (status.status === 'completed') {
      // Get results
      const { data: results } = await client.get(`/api/scan/${scan.scan_id}/results`);

      console.log(`\nScan completed!`);
      console.log(`Total findings: ${results.summary.total_findings}`);
      console.log(`Critical: ${results.summary.critical}`);
      console.log(`High: ${results.summary.high}`);

      // Filter critical/high findings
      const critical = results.findings.filter(f =>
        f.severity === 'critical' || f.severity === 'high'
      );

      critical.forEach(finding => {
        console.log(`\n⚠️  ${finding.severity.toUpperCase()}: ${finding.title}`);
        console.log(`   ${finding.affected_component.url}`);
      });
    }
  } catch (error) {
    console.error('Error:', error.response?.data || error.message);
  }
}

runScan();
```

### cURL

```bash
#!/bin/bash

API_KEY="xeops_live_your_api_key"
BASE_URL="https://api.xeops.ai"

# Create scan
SCAN_RESPONSE=$(curl -s -X POST "$BASE_URL/api/scan" \
  -H "Authorization: Bearer $API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "target": "https://api.example.com",
    "scan_type": "standard",
    "description": "Weekly security audit"
  }')

SCAN_ID=$(echo $SCAN_RESPONSE | jq -r '.scan_id')
echo "Scan created: $SCAN_ID"

# Poll for completion
while true; do
  STATUS_RESPONSE=$(curl -s "$BASE_URL/api/scan/$SCAN_ID" \
    -H "Authorization: Bearer $API_KEY")

  STATUS=$(echo $STATUS_RESPONSE | jq -r '.status')
  PROGRESS=$(echo $STATUS_RESPONSE | jq -r '.progress')

  echo "Status: $STATUS ($PROGRESS%)"

  if [ "$STATUS" = "completed" ] || [ "$STATUS" = "failed" ]; then
    break
  fi

  sleep 30
done

# Get results
if [ "$STATUS" = "completed" ]; then
  curl -s "$BASE_URL/api/scan/$SCAN_ID/results" \
    -H "Authorization: Bearer $API_KEY" | jq '.summary'
fi
```

---

## 🔄 CI/CD Integration

### GitHub Actions

```yaml
name: Security Scan

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    - cron: '0 0 * * 0' # Weekly on Sunday

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger XeOps Scan
        run: |
          RESPONSE=$(curl -s -X POST https://api.xeops.ai/api/scan \
            -H "Authorization: Bearer ${{ secrets.XEOPS_API_KEY }}" \
            -H "Content-Type: application/json" \
            -d '{
              "target": "${{ secrets.STAGING_URL }}",
              "scan_type": "standard",
              "description": "CI/CD security scan - ${{ github.sha }}"
            }')

          SCAN_ID=$(echo $RESPONSE | jq -r '.scan_id')
          echo "SCAN_ID=$SCAN_ID" >> $GITHUB_ENV

      - name: Wait for Scan Completion
        run: |
          while true; do
            STATUS=$(curl -s https://api.xeops.ai/api/scan/$SCAN_ID \
              -H "Authorization: Bearer ${{ secrets.XEOPS_API_KEY }}" \
              | jq -r '.status')

            if [ "$STATUS" = "completed" ] || [ "$STATUS" = "failed" ]; then
              break
            fi

            sleep 30
          done

      - name: Check Results
        run: |
          RESULTS=$(curl -s https://api.xeops.ai/api/scan/$SCAN_ID/results \
            -H "Authorization: Bearer ${{ secrets.XEOPS_API_KEY }}")

          CRITICAL=$(echo $RESULTS | jq -r '.summary.critical')
          HIGH=$(echo $RESULTS | jq -r '.summary.high')

          echo "Critical vulnerabilities: $CRITICAL"
          echo "High vulnerabilities: $HIGH"

          if [ "$CRITICAL" -gt 0 ]; then
            echo "❌ Critical vulnerabilities found! Failing build."
            exit 1
          fi
```

### GitLab CI

```yaml
security_scan:
  stage: test
  script:
    - |
      RESPONSE=$(curl -s -X POST https://api.xeops.ai/api/scan \
        -H "Authorization: Bearer $XEOPS_API_KEY" \
        -H "Content-Type: application/json" \
        -d "{
          \"target\": \"$STAGING_URL\",
          \"scan_type\": \"standard\",
          \"description\": \"CI/CD scan - $CI_COMMIT_SHA\"
        }")

      SCAN_ID=$(echo $RESPONSE | jq -r '.scan_id')

      while true; do
        STATUS=$(curl -s https://api.xeops.ai/api/scan/$SCAN_ID \
          -H "Authorization: Bearer $XEOPS_API_KEY" \
          | jq -r '.status')

        if [ "$STATUS" = "completed" ] || [ "$STATUS" = "failed" ]; then
          break
        fi

        sleep 30
      done

      RESULTS=$(curl -s https://api.xeops.ai/api/scan/$SCAN_ID/results \
        -H "Authorization: Bearer $XEOPS_API_KEY")

      CRITICAL=$(echo $RESULTS | jq -r '.summary.critical')

      if [ "$CRITICAL" -gt 0 ]; then
        echo "❌ Critical vulnerabilities found!"
        exit 1
      fi
  only:
    - main
    - merge_requests
```

---

## 📞 Support

**API Questions?**
- Email: api-support@xeops.ai
- Documentation: https://docs.xeops.ai
- Status: https://status.xeops.ai

**Report API Issues:**
- GitHub: https://github.com/xeops-sofyen/xeops/issues
- Email: support@xeops.ai

---

**Happy Scanning! 🚀**
