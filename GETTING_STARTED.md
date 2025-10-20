# 🚀 Getting Started with XeOps.ai

Welcome to XeOps.ai! This guide will help you get started with our AI-powered cybersecurity platform in minutes.

---

## 📋 Table of Contents

1. [Create Your Account](#create-your-account)
2. [Your First Security Scan](#your-first-security-scan)
3. [Understanding Results](#understanding-results)
4. [Dashboard Overview](#dashboard-overview)
5. [Plans & Pricing](#plans--pricing)
6. [FAQ](#faq)

---

## 🎯 Create Your Account

### Step 1: Sign Up

1. Visit [xeops.ai](https://xeops.ai)
2. Click **"Sign Up"** in the top right
3. Fill in your information:
   - Email address
   - Password (minimum 8 characters)
   - First name & Last name
   - Company name
4. Click **"Create Account"**

### Step 2: Verify Your Email

1. Check your email inbox
2. Click the verification link
3. Your account is now active!

### Step 3: Login

1. Go to [xeops.ai/login](https://xeops.ai/login)
2. Enter your email and password
3. You'll be redirected to your dashboard

---

## 🔍 Your First Security Scan

### Option A: Free Scan (No Account Required)

Perfect for trying out XeOps without commitment.

1. Visit [xeops.ai/scan](https://xeops.ai/scan)
2. Fill in the scan request form:
   ```
   Email: your@email.com
   Company: Your Company Name
   Target URL or API: https://your-app.com
   Industry: Select your industry
   Urgency: Normal / Urgent
   ```
3. Click **"Request Free Scan"**
4. Our team will review and send you results within 24-48 hours

### Option B: Instant Scan (Requires Account)

For immediate results and full features.

1. **Login** to your dashboard
2. Click **"New Scan"** button
3. Configure your scan:

   **Basic Settings:**
   ```
   Target URL: https://your-app.com
   Scan Type: Quick / Standard / Deep
   Description: What are you testing?
   ```

   **Advanced Settings (Optional):**
   ```
   Authentication:
     - API Key
     - Bearer Token
     - Basic Auth

   Scan Intensity:
     - Light (fastest, surface-level)
     - Normal (balanced, recommended)
     - Aggressive (thorough, may impact performance)

   Scan Scope:
     - Specific endpoints
     - Entire domain
     - Subdomain inclusion
   ```

4. Click **"Start Scan"**
5. Watch real-time progress in your dashboard

---

## 📊 Understanding Results

### Severity Levels

XeOps classifies vulnerabilities using industry-standard severity ratings:

| Severity | CVSS Score | Risk Level | Action Required |
|----------|------------|------------|-----------------|
| 🔴 **Critical** | 9.0-10.0 | Severe | Fix immediately |
| 🟠 **High** | 7.0-8.9 | Major | Fix within 7 days |
| 🟡 **Medium** | 4.0-6.9 | Moderate | Fix within 30 days |
| 🟢 **Low** | 0.1-3.9 | Minor | Fix when convenient |
| 🔵 **Info** | 0.0 | Informational | No immediate action |

### Vulnerability Report Structure

Each finding includes:

**1. Overview**
```
Title: SQL Injection in login endpoint
Severity: Critical (CVSS 9.8)
CWE: CWE-89
Status: Open
```

**2. Description**
- What the vulnerability is
- How it was discovered
- Affected endpoint/component

**3. Impact**
- Potential consequences
- Attack scenarios
- Business risk assessment

**4. Proof of Concept (PoC)**
```bash
# Example exploit code
curl -X POST https://api.example.com/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin'\'' OR 1=1--","password":"anything"}'
```

**5. Remediation**
- Step-by-step fix instructions
- Code examples
- Best practices
- Resources for learning

**6. References**
- OWASP guidelines
- CVE details
- CWE information
- Security advisories

---

## 🎛️ Dashboard Overview

### Main Dashboard

Your central hub for all security activities.

**Key Metrics:**
- 📊 Total scans performed
- 🔍 Active scans in progress
- 🐛 Total vulnerabilities found
- 🚨 Critical issues requiring attention

**Quick Actions:**
- ➕ New Scan
- 📈 View Reports
- 👤 Profile Settings

### Scans Page

View and manage all your security scans.

**Table Columns:**
- Target URL
- Scan type
- Status (Running / Completed / Failed)
- Findings count
- Created date
- Actions (View / Download / Delete)

**Filters:**
- Date range
- Status
- Severity
- Scan type

### Reports Page

Access detailed vulnerability reports.

**Report Formats:**
- 📄 PDF (Executive summary)
- 📊 Excel (Detailed findings)
- 🗂️ JSON (API integration)
- 📝 HTML (Interactive dashboard)

**Report Sections:**
- Executive summary
- Vulnerability breakdown
- Risk assessment
- Remediation roadmap
- Compliance checklist (OWASP, MITRE)

### Profile Settings

Manage your account and preferences.

**Account Information:**
- Email address
- Name and company
- Subscription plan
- Usage statistics

**Security Settings:**
- Change password
- Two-factor authentication (coming soon)
- API keys
- Session management

**Notifications:**
- Email alerts for scan completion
- Critical vulnerability notifications
- Weekly security digest
- Product updates

---

## 💰 Plans & Pricing

### Free Tier

Perfect for trying out XeOps.

**Includes:**
- ✅ 1 free scan per month
- ✅ Basic vulnerability detection
- ✅ 7-day result retention
- ✅ Email support

**Limitations:**
- ⏱️ 24-48 hour processing time
- 📊 Basic reports only
- 🔒 No API access

### Professional Plan

**€49/month** or **€490/year** (save 17%)

**Includes:**
- ✅ 10 scans per month
- ✅ Instant scan execution
- ✅ AI-powered analysis
- ✅ Advanced vulnerability detection (500+ types)
- ✅ Real-time progress tracking
- ✅ 90-day result retention
- ✅ Priority email support
- ✅ API access (100 requests/day)
- ✅ Custom scan configurations
- ✅ PDF, Excel, JSON reports

**Best for:**
- Startups and SMBs
- Individual developers
- Bug bounty hunters
- Small security teams

### Enterprise Plan

**Custom Pricing** - Contact sales@xeops.ai

**Includes everything in Professional, plus:**
- ✅ Unlimited scans
- ✅ Custom scan intensity
- ✅ Dedicated AI models
- ✅ White-label reports
- ✅ SSO integration
- ✅ Compliance reporting (SOC2, ISO 27001)
- ✅ Dedicated account manager
- ✅ SLA guarantee (99.9% uptime)
- ✅ On-premise deployment option
- ✅ API access (unlimited)
- ✅ Custom integrations (Jira, Slack, etc.)

**Best for:**
- Large enterprises
- Security consulting firms
- Managed security service providers (MSSPs)
- Organizations with compliance requirements

---

## ❓ FAQ

### General Questions

**Q: How accurate is XeOps?**
> A: XeOps has a 99.9% accuracy rate with 0% false positives, validated through real bug bounty programs.

**Q: What types of vulnerabilities can XeOps detect?**
> A: XeOps covers 500+ vulnerability types including OWASP Top 10, API security issues, authentication flaws, and custom AI-discovered vulnerabilities.

**Q: How long does a scan take?**
> A:
> - Quick scan: 5-10 minutes
> - Standard scan: 15-30 minutes
> - Deep scan: 30-60 minutes
>
> Times vary based on target complexity.

**Q: Can I scan any website?**
> A: You must have authorization to scan the target. Unauthorized scanning is illegal and violates our Terms of Service.

**Q: Is my data secure?**
> A: Yes. All data is encrypted in transit (TLS 1.3) and at rest (AES-256). We're compliant with GDPR and follow industry best practices.

### Technical Questions

**Q: What technologies does XeOps support?**
> A: We support web applications, REST APIs, GraphQL, SOAP, mobile app backends, and cloud infrastructure.

**Q: Can XeOps scan authenticated endpoints?**
> A: Yes! You can provide API keys, bearer tokens, or basic auth credentials for authenticated scanning.

**Q: Does XeOps integrate with CI/CD?**
> A: Yes. Professional and Enterprise plans include API access for CI/CD integration.

**Q: Can I automate scans?**
> A: Yes. Use our REST API to trigger scans programmatically:
> ```bash
> curl -X POST https://api.xeops.ai/api/scan \
>   -H "Authorization: Bearer YOUR_API_KEY" \
>   -H "Content-Type: application/json" \
>   -d '{"target":"https://your-app.com","scan_type":"standard"}'
> ```

**Q: What's the difference between scan types?**
> A:
> - **Quick**: Fast surface-level check (OWASP Top 10 basics)
> - **Standard**: Comprehensive testing (recommended for most use cases)
> - **Deep**: Aggressive testing with all checks (may impact performance)

### Billing Questions

**Q: Can I cancel anytime?**
> A: Yes. No long-term contracts. Cancel anytime from your dashboard.

**Q: Do unused scans roll over?**
> A: No. Scan quotas reset monthly. However, Enterprise customers can request custom rollover policies.

**Q: What payment methods do you accept?**
> A: We accept credit cards (Visa, Mastercard, Amex), PayPal, and bank transfers (Enterprise only).

**Q: Is there a free trial?**
> A: Yes! Every account includes 1 free scan per month. No credit card required.

**Q: Can I get a refund?**
> A: We offer a 30-day money-back guarantee for annual plans. Monthly subscriptions are non-refundable.

---

## 🆘 Need Help?

### Support Channels

**📧 Email Support:**
- General inquiries: contact@xeops.ai
- Technical support: support@xeops.ai
- Sales: sales@xeops.ai
- Security issues: security@xeops.ai

**📚 Documentation:**
- [API Reference](https://docs.xeops.ai/api)
- [Video Tutorials](https://xeops.ai/tutorials)
- [Blog & Guides](https://xeops.ai/blog)

**💬 Community:**
- [GitHub Discussions](https://github.com/xeops-sofyen/xeops/discussions)
- [LinkedIn](https://www.linkedin.com/company/xeops)

**Response Times:**
- Free tier: 48 hours
- Professional: 24 hours
- Enterprise: 4 hours (SLA guaranteed)

---

## 🎓 Next Steps

Now that you're set up, here's what to do next:

1. ✅ **Run your first scan** - Test a safe environment first
2. ✅ **Explore the dashboard** - Familiarize yourself with all features
3. ✅ **Read a sample report** - Understand how to interpret results
4. ✅ **Set up notifications** - Get alerts for important findings
5. ✅ **Join our community** - Connect with other security professionals

---

## 📖 Additional Resources

- [Security Best Practices Guide](./SECURITY_BEST_PRACTICES.md)
- [API Integration Guide](./API_GUIDE.md)
- [Vulnerability Remediation Guide](./REMEDIATION_GUIDE.md)
- [Compliance Checklist](./COMPLIANCE.md)

---

**Welcome to the future of cybersecurity! 🚀**

*If you have any questions, we're here to help: support@xeops.ai*
