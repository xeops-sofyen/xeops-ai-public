# 🚀 Getting Started with XeOps.ai

Welcome to **XeOps.ai** - the AI-powered offensive security platform that transforms vulnerability discovery into actionable exploits automatically.

This guide will help you get started in **less than 5 minutes**.

---

## 📋 Table of Contents

1. [Free Trial - No Credit Card Required](#-free-trial---no-credit-card-required)
2. [Create Your Account](#-create-your-account)
3. [Your First Security Scan](#-your-first-security-scan)
4. [Understanding Results](#-understanding-results)
5. [Dashboard Overview](#-dashboard-overview)
6. [Plans & Pricing](#-plans--pricing)
7. [API Integration](#-api-integration)
8. [FAQ](#-faq)

---

## 🎁 Free Trial - No Credit Card Required

XeOps offers **10 free scans** to test the platform. Start immediately without any payment information.

### What's Included in Free Trial?

- ✅ 10 vulnerability scans
- ✅ Full platform access
- ✅ OWASP Top 10 coverage
- ✅ Basic compliance reports
- ✅ AI security expert chatbot
- ✅ Proof-of-concept exploits
- ❌ No credit card required
- ❌ No time limit

**[Start Your Free Scan →](https://www.xeops.ai)**

---

## 🎯 Create Your Account

### Step 1: Sign Up

1. Visit [www.xeops.ai/signup](https://www.xeops.ai/signup)
2. Fill in your information:
   - **Email address** (work email recommended)
   - **Password** (minimum 8 characters, must include uppercase, lowercase, and number)
   - **First name** & **Last name**
   - **Company name** (optional but recommended)
3. Click **"Create Account"**

### Step 2: Verify Your Email

1. Check your email inbox for a verification email from `noreply@xeops.ai`
2. Click the verification link (valid for 24 hours)
3. Your account is now active! 🎉

**Troubleshooting**:
- **Didn't receive email?** Check your spam/junk folder
- **Link expired?** Request a new verification email from the login page
- **Still stuck?** Contact support@xeops.ai

### Step 3: Complete Your Profile

After email verification, you'll be prompted to:

1. **Choose your role**: Bug Bounty Hunter, Security Engineer, DevSecOps, Red Team, etc.
2. **Set your preferences**: Scan intensity, notification settings
3. **Skip the tour** or take a quick platform walkthrough

---

## 🔍 Your First Security Scan

### Option A: Quick Scan (Recommended for First-Time Users)

Perfect for testing the platform quickly.

1. **Click "New Scan"** in the dashboard
2. **Enter your target**:
   ```
   Target URL: https://your-application.com
   ```
3. **Choose scan type**: Select **"Quick Scan"** for your first test
4. **Click "Start Scan"**

**Duration**: 5-10 minutes

**Coverage**:
- ✅ OWASP Top 10 basics
- ✅ Common vulnerabilities
- ✅ Basic PoC generation

---

### Option B: Full Scan (Comprehensive Testing)

For complete security assessment.

1. **Click "New Scan"** in the dashboard
2. **Configure your scan**:

   **Basic Settings:**
   ```
   Target URL: https://your-application.com
   Scan Name: Production App Security Audit
   Description: Comprehensive security assessment
   ```

   **Advanced Settings:**
   ```
   Scan Type: Full (Web + API + Mobile)
   Intensity: Normal (recommended) or Aggressive

   Attack Surfaces:
   ☑ Web Application
   ☑ REST API
   ☑ GraphQL endpoints
   ☑ Mobile API (if applicable)
   ☑ Cloud infrastructure checks
   ```

   **Authentication (Optional):**
   ```
   ☑ Enable authenticated scanning
   Auth Type: Bearer Token / API Key / Basic Auth / Cookie
   Credentials: [Your test account credentials]
   ```

   **Scan Scope:**
   ```
   Include subdomains: Yes / No
   Max crawl depth: 5 (default)
   Concurrent requests: Auto / 10 / 20 / 50
   ```

3. **Click "Start Scan"**

**Duration**: 15-45 minutes (depending on target size)

**Coverage**:
- ✅ Full OWASP Top 10
- ✅ Business logic flaws
- ✅ Authentication/Authorization issues
- ✅ API-specific vulnerabilities
- ✅ Cloud misconfigurations
- ✅ Custom exploit generation
- ✅ Verified PoC for all findings

---

### Option C: Scheduled Scans (CI/CD Integration)

Automate security testing in your deployment pipeline.

1. **Go to "Integrations"** in settings
2. **Choose your CI/CD tool**: Jenkins, GitLab, GitHub Actions, CircleCI
3. **Copy the API key** provided
4. **Add to your pipeline**:

```yaml
# Example: GitHub Actions
- name: XeOps Security Scan
  run: |
    curl -X POST https://api.xeops.ai/api/scan \
      -H "Authorization: Bearer ${{ secrets.XEOPS_API_KEY }}" \
      -H "Content-Type: application/json" \
      -d '{
        "target": "${{ secrets.STAGING_URL }}",
        "scan_type": "full",
        "fail_on_severity": "high"
      }'
```

---

## 📊 Understanding Results

### Severity Levels

XeOps uses industry-standard CVSS scoring:

| Severity | CVSS Score | Icon | Action Required |
|----------|------------|------|-----------------|
| **Critical** | 9.0-10.0 | 🔴 | Fix immediately (24h) |
| **High** | 7.0-8.9 | 🟠 | Fix within 7 days |
| **Medium** | 4.0-6.9 | 🟡 | Fix within 30 days |
| **Low** | 0.1-3.9 | 🟢 | Fix when convenient |
| **Info** | 0.0 | 🔵 | No immediate action |

---

### Vulnerability Report Structure

Each finding includes:

#### 1. Overview
```
Title: SQL Injection in User Login Endpoint
Severity: Critical (CVSS 9.8)
CWE: CWE-89
CVE: CVE-2024-XXXXX (if applicable)
Status: Open / In Progress / Fixed / False Positive
```

#### 2. Description
- What the vulnerability is
- How it was discovered
- Affected component (URL, parameter, method)

#### 3. Impact
```
Business Impact: HIGH
- Unauthorized database access
- Data breach risk (user PII, passwords)
- Potential full system compromise

Technical Impact:
- SQL injection allows arbitrary database queries
- Bypasses authentication completely
- Enables privilege escalation
```

#### 4. Proof of Concept (PoC)
```bash
# Working exploit code
curl -X POST https://api.example.com/login \
  -H "Content-Type: application/json" \
  -d '{
    "username": "admin'\'' OR 1=1--",
    "password": "anything"
  }'

# Response: 200 OK
# { "token": "eyJhbGc...", "user": "admin" }
```

#### 5. Remediation
```
Priority: CRITICAL - Fix within 24 hours

Step-by-step fix:
1. Replace string concatenation with parameterized queries
2. Use prepared statements/ORM
3. Implement input validation

Code example (before):
const query = `SELECT * FROM users WHERE username='${username}'`;

Code example (after):
const query = 'SELECT * FROM users WHERE username = ?';
db.query(query, [username]);

Additional security measures:
- Implement rate limiting on login endpoint
- Add WAF rules to block SQL injection patterns
- Enable database query logging
```

#### 6. References
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [CWE-89: SQL Injection](https://cwe.mitre.org/data/definitions/89.html)
- [NIST NVD](https://nvd.nist.gov/)

---

### Export Formats

Download your findings in multiple formats:

- **PDF Report** - Executive summary for stakeholders
- **JSON** - API integration and automation
- **CSV** - Spreadsheet analysis
- **SARIF** - GitHub Security tab integration
- **HTML** - Interactive web report

---

## 🎛️ Dashboard Overview

### Main Dashboard

Your security command center.

**Key Metrics:**
```
📊 Total Scans: 47
🔍 Active Scans: 2
🐛 Total Vulnerabilities: 127
🚨 Critical Issues: 3 (action required!)
```

**Quick Actions:**
- ➕ **New Scan** - Start vulnerability assessment
- 📈 **View All Scans** - Browse scan history
- 💬 **AI Security Expert** - Ask security questions
- ⚙️ **Settings** - Configure integrations

---

### Scans Page

View and manage all security scans.

**Table Columns:**
| Column | Description |
|--------|-------------|
| **Target** | Scanned URL/application |
| **Scan Type** | Quick / Full / Custom |
| **Status** | Queued / Running / Completed / Failed |
| **Findings** | 🔴 Critical, 🟠 High, 🟡 Medium, 🟢 Low |
| **Created** | Scan start time |
| **Actions** | View / Export / Re-scan / Delete |

**Filters:**
- Date range (Last 7 days, Last 30 days, Custom)
- Status (All, Completed, Running, Failed)
- Severity (Critical, High, Medium+)
- Scan type

---

### AI Security Expert

Real-time chatbot for vulnerability insights.

**What you can ask:**
- "Explain this SQL injection vulnerability"
- "What's the best way to fix XSS in React?"
- "Is CSRF token validation necessary for my API?"
- "How severe is this business logic flaw?"
- "Generate a remediation plan for my critical findings"

**Available in all plans** (usage limits apply).

---

### Integrations

Connect XeOps with your existing tools.

**Available Integrations:**

| Tool | Type | Purpose |
|------|------|---------|
| **Slack** | Notifications | Real-time scan alerts |
| **JIRA** | Issue Tracking | Auto-create tickets for vulnerabilities |
| **GitHub** | CI/CD | Security scanning in pull requests |
| **GitLab** | CI/CD | Pipeline integration |
| **Jenkins** | CI/CD | Automated security tests |
| **Webhook** | Custom | Send results to any endpoint |

---

## 💰 Plans & Pricing

### 🎁 Free Trial
- **10 free scans**
- No credit card required
- Full platform access
- Basic compliance reports

---

### 💼 Starter Plan - €49/month

**Perfect for:**
- Startups
- Small security teams
- Bug bounty hunters

**Includes:**
- ✅ **100 scans/month**
- ✅ **5 team members**
- ✅ Web & API vulnerability scanning
- ✅ OWASP Top 10 coverage
- ✅ Custom exploit generation
- ✅ Basic compliance reports (PDF)
- ✅ API access
- ✅ 48-hour email support

**Best for**: Small teams starting with automated security testing.

**[Start Starter Plan →](https://www.xeops.ai/pricing)**

---

### 🚀 Professional Plan - €149/month (Most Popular)

**Perfect for:**
- Growing companies
- Security teams
- DevSecOps engineers

**Includes:**
- ✅ **500 scans/month**
- ✅ **20 team members**
- ✅ All attack surfaces (Web, API, Mobile, Cloud)
- ✅ Verified PoC exploits
- ✅ Full compliance reports (SOC 2, ISO 27001, PCI-DSS)
- ✅ API access + Webhooks
- ✅ Integrations: Slack, JIRA, GitHub
- ✅ 24-hour priority support

**Best for**: Teams needing comprehensive security automation with compliance reporting.

**[Start Professional Plan →](https://www.xeops.ai/pricing)**

---

### 🏢 Enterprise Plan - €499/month

**Perfect for:**
- Large enterprises
- MSSPs
- Advanced security teams

**Includes:**
- ✅ **Unlimited scans & team members**
- ✅ Web3 & blockchain testing
- ✅ APT red team simulation
- ✅ White-box + black-box analysis
- ✅ White-label reports (custom branding)
- ✅ Custom integrations & SSO
- ✅ Dedicated account manager
- ✅ 24/7 support (4-hour SLA)

**Best for**: Enterprises requiring unlimited scanning, custom branding, and premium support.

**[Contact Sales →](mailto:sales@xeops.ai)**

---

## 🔌 API Integration

Integrate XeOps into your security workflow.

### Quick Start

```bash
# 1. Get your API key from dashboard settings
# 2. Make your first API call

curl -X POST https://api.xeops.ai/api/scan \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "target": "https://your-app.com",
    "scan_type": "full",
    "description": "Automated security scan"
  }'
```

### Full API Documentation

For complete API reference, see [API_GUIDE.md](./API_GUIDE.md).

**Key endpoints:**
- `POST /api/scan` - Create new scan
- `GET /api/scan/:id` - Get scan status
- `GET /api/scan/:id/results` - Get findings
- `GET /api/scans` - List all scans
- `DELETE /api/scan/:id` - Cancel scan

---

## ❓ FAQ

### General Questions

**Q: How accurate is XeOps?**
> XeOps achieves **zero false positives** by verifying every finding with a working proof-of-concept exploit. Traditional scanners have 20-40% false positive rates.

**Q: What types of vulnerabilities can XeOps detect?**
> We cover **60,000+ vulnerability types** including:
> - OWASP Top 10
> - API security issues (OWASP API Top 10)
> - Business logic flaws
> - Authentication/Authorization issues
> - Cloud misconfigurations (AWS, GCP, Azure)
> - Mobile app vulnerabilities
> - Web3/smart contract issues (Enterprise)

**Q: How long does a scan take?**
> - **Quick scan**: 5-10 minutes
> - **Standard scan**: 15-30 minutes
> - **Deep scan**: 30-60 minutes
>
> Times vary based on target complexity and size.

**Q: Can I scan any website?**
> ⚠️ **Important**: You must have **written authorization** to scan a target. Unauthorized scanning is **illegal** and violates our Terms of Service.
>
> Only scan:
> - Your own applications
> - Client applications (with written permission)
> - Bug bounty programs (within scope)

**Q: Is my data secure?**
> Yes. XeOps implements enterprise-grade security:
> - ✅ All data encrypted in transit (TLS 1.3)
> - ✅ All data encrypted at rest (AES-256)
> - ✅ GDPR compliant
> - ✅ SOC 2 Type II certified (in progress)
> - ✅ No data sharing with third parties
> - ✅ Automatic data deletion after 90 days (configurable)

---

### Technical Questions

**Q: What technologies does XeOps support?**
> We test:
> - **Web apps**: PHP, Node.js, Python, Ruby, Java, .NET, Go
> - **APIs**: REST, GraphQL, SOAP, gRPC
> - **Mobile**: iOS, Android native apps and APIs
> - **Cloud**: AWS, GCP, Azure infrastructure
> - **Web3**: Ethereum, Solana, Polygon smart contracts (Enterprise)
> - **Databases**: PostgreSQL, MySQL, MongoDB, Redis

**Q: Can XeOps scan authenticated endpoints?**
> Yes! Provide credentials in multiple formats:
> - API keys
> - Bearer tokens (JWT, OAuth)
> - Basic authentication
> - Session cookies
> - Multi-factor authentication (with TOTP)

**Q: Does XeOps integrate with CI/CD?**
> Yes. Professional and Enterprise plans include:
> - Jenkins plugin
> - GitLab CI/CD integration
> - GitHub Actions workflow
> - CircleCI orb
> - Custom webhook for any platform

**Q: Can I automate scans?**
> Absolutely. Use our REST API:
> ```bash
> curl -X POST https://api.xeops.ai/api/scan \
>   -H "Authorization: Bearer YOUR_API_KEY" \
>   -H "Content-Type: application/json" \
>   -d '{"target":"https://your-app.com","scan_type":"full"}'
> ```
> See [API_GUIDE.md](./API_GUIDE.md) for full documentation.

**Q: What's the difference between scan types?**
> - **Quick**: Fast surface-level check (OWASP Top 10 basics) - 5-10 min
> - **Standard**: Comprehensive testing (recommended) - 15-30 min
> - **Deep**: Aggressive testing with all checks (may impact performance) - 30-60 min

---

### Billing Questions

**Q: Can I cancel anytime?**
> Yes. No long-term contracts. Cancel anytime from your dashboard. Pro-rated refunds available for annual plans.

**Q: Do unused scans roll over?**
> No. Scan quotas reset monthly. However, **Enterprise customers** can request custom rollover policies.

**Q: What payment methods do you accept?**
> - Credit cards (Visa, Mastercard, Amex, Discover)
> - PayPal
> - Bank transfers (Enterprise only, annual plans)

**Q: Is there a free trial?**
> Yes! **10 free scans** included with every account. No credit card required.

**Q: Can I get a refund?**
> - **Monthly plans**: Non-refundable (cancel anytime)
> - **Annual plans**: 30-day money-back guarantee
> - **Enterprise**: Custom terms negotiable

---

## 🆘 Need Help?

### Support Channels

**📧 Email Support:**
- General inquiries: contact@xeops.ai
- Technical support: support@xeops.ai
- Sales questions: sales@xeops.ai
- Security issues: security@xeops.ai

**📚 Resources:**
- [Full Documentation](https://www.xeops.ai/docs)
- [API Reference](./API_GUIDE.md)
- [Video Tutorials](https://www.xeops.ai/tutorials)
- [Blog & Security Guides](https://www.xeops.ai/blog)

**💬 Community:**
- [GitHub Discussions](https://github.com/xeops-sofyen/xeops-ai-public/discussions)
- [LinkedIn](https://www.linkedin.com/company/xeops)

**Response Times:**
- **Free trial**: 72 hours
- **Starter**: 48 hours
- **Professional**: 24 hours (priority)
- **Enterprise**: 4 hours (SLA guaranteed)

---

## 🎓 Next Steps

Now that you're set up, here's what to do next:

1. ✅ **Run your first scan** - Start with a safe test environment
2. ✅ **Explore the dashboard** - Familiarize yourself with all features
3. ✅ **Review a sample report** - Understand vulnerability findings
4. ✅ **Set up integrations** - Connect Slack, JIRA, or GitHub
5. ✅ **Configure API access** - Automate security testing
6. ✅ **Join our community** - Connect with other security professionals

---

## 📖 Additional Resources

- [API Integration Guide](./API_GUIDE.md) - Complete API documentation
- [Security Best Practices](https://www.xeops.ai/docs/security) - Secure scanning guidelines
- [Compliance Guide](https://www.xeops.ai/docs/compliance) - SOC 2, ISO 27001, PCI-DSS
- [Video Tutorials](https://www.xeops.ai/tutorials) - Step-by-step walkthroughs

---

<div align="center">

## 🚀 Ready to Start?

[![Start Free Scan](https://img.shields.io/badge/Start_Free_Scan-10_Scans_Free-00C853?style=for-the-badge)](https://www.xeops.ai)
[![View Pricing](https://img.shields.io/badge/View-Pricing-FF0137?style=for-the-badge)](https://www.xeops.ai/pricing)

**From Discovery to Exploit, Automatically**

*Questions? Email us at support@xeops.ai*

</div>
