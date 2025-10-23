# 🛡️ XeOps Guardian - VS Code Extension

<div align="center">

![XeOps Guardian Banner](https://via.placeholder.com/800x200/06090A/FF0137?text=XeOps+Guardian+-+Security+While+You+Code)

**The First Offensive Security Extension for VS Code**

[![Install](https://img.shields.io/badge/Install-VS_Code_Marketplace-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian)
[![Downloads](https://img.shields.io/visual-studio-marketplace/d/xeops.xeops-guardian?style=for-the-badge&label=Downloads)](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian)
[![Rating](https://img.shields.io/visual-studio-marketplace/r/xeops.xeops-guardian?style=for-the-badge&label=Rating)](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian)

**Ship secure code from day one** · **Zero context switching** · **AI-powered**

[📥 Install Now](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian) • [🔑 Get API Key](https://xeops.ai/dashboard) • [📖 Documentation](./docs/vscode-extension/)

</div>

---

## 🌟 Why XeOps Guardian?

### The Problem

Developers discover security vulnerabilities **AFTER deployment**:
- ❌ Security audits happen too late
- ❌ CI/CD security gates slow down shipping
- ❌ Context switching between code editor and security tools
- ❌ Learning curve for security concepts

### The Solution

**Security WHILE you code**, directly in VS Code:
- ✅ Real-time vulnerability detection as you type
- ✅ AI-powered fix suggestions (like Copilot, but for security)
- ✅ Zero context switching - everything in your editor
- ✅ Learn security principles while coding

> **"GitHub Copilot suggests code. XeOps Guardian secures it."**

---

## 🎯 Key Features

### 🛡️ Defense Mode - Secure Your Code

**Real-Time Vulnerability Detection**
```javascript
// You type this
app.get('/user', (req, res) => {
  const id = req.query.id;
  db.query(`SELECT * FROM users WHERE id = ${id}`);  // 🔴 SQL Injection detected
});

// XeOps underlines the vulnerability in red
// Hover to see: "Critical: SQL Injection vulnerability"
```

**AI-Powered Auto-Fix**
```javascript
// Press Ctrl+. on the underlined code
// XeOps suggests:
db.query('SELECT * FROM users WHERE id = $1', [id]);  // ✅ Fixed with parameterized query
```

**Security Score Per File**
```
file.js:  A+  (No vulnerabilities)
auth.js:  C   (2 medium, 1 low)
api.js:   F   (1 critical, 3 high)
```

### ⚔️ Offense Mode - Test & Exploit

**Generate Custom Exploits**
- Select vulnerable code
- Right-click → "XeOps: Generate Exploit"
- Get working PoC in seconds

**Example:**
```sql
-- Detected: SQL Injection on line 42
-- Generated exploit:
https://api.com/user?id=1' UNION SELECT password FROM users--
```

**Test in Sandbox**
- Click "Test Exploit"
- XeOps runs exploit in isolated Docker container
- See real-time results

### 🤖 AI Security Chat

Ask questions directly in VS Code:
```
You: "Is this authentication bypass possible?"
XeOps AI: "Yes, the JWT token validation is missing..."

You: "Generate a payload to test this XSS"
XeOps AI: "<script>alert(document.cookie)</script>"
```

Powered by **XeOps.AI® Advanced AI Agent**.

### 🎯 Attack Path Visualization

See how attackers would chain vulnerabilities:
```
SQL Injection (line 42)
  ↓
Extract admin password
  ↓
Authentication bypass (line 78)
  ↓
Privilege escalation
  ↓
Full system compromise
```

---

## 📦 Installation (2 minutes)

### Step 1: Install Extension

**From VS Code:**
1. Open Extensions (`Ctrl+Shift+X`)
2. Search "XeOps Guardian"
3. Click Install

**Or from command line:**
```bash
code --install-extension xeops.xeops-guardian
```

### Step 2: Get API Key

1. Go to [xeops.ai/dashboard](https://xeops.ai/dashboard)
2. Sign up (free - 10 scans included)
3. Navigate to **Settings** → **API Keys**
4. Copy your API key

### Step 3: Configure

1. Open VS Code Settings (`Ctrl+,`)
2. Search "XeOps"
3. Paste your API key in `xeops.apiKey`
4. Choose mode: `Defense` or `Offense`

### Step 4: Start Scanning!

- **Scan current file**: `Ctrl+Shift+X S`
- **Switch mode**: `Ctrl+Shift+X M`
- **Open AI chat**: `Ctrl+Shift+X C`

---

## 💰 Pricing

### Free Plan (10 Scans/Month)
Perfect for trying out the extension:
- ✅ 10 scans/month
- ✅ Defense mode (vulnerability detection)
- ✅ AI chat (10 messages/month)
- ✅ Community support

**No credit card required** - [Get Started](https://xeops.ai/dashboard)

### Pro Plan ($29/month)
For serious developers:
- ✅ **Unlimited scans**
- ✅ Offense mode (exploit generation)
- ✅ Attack path visualization
- ✅ Bug bounty integration
- ✅ Priority support

### Enterprise (Custom)
For teams:
- ✅ Everything in Pro
- ✅ Team collaboration
- ✅ Custom AI models
- ✅ SSO/SAML
- ✅ Dedicated support

**[View Pricing](https://xeops.ai/pricing)** • **[Contact Sales](mailto:sales@xeops.ai)**

---

## 🎬 Demo

### Watch XeOps Guardian in Action

[![Demo Video](https://img.shields.io/badge/▶️-Watch_Demo-FF0137?style=for-the-badge)](https://youtube.com/watch?v=DEMO_VIDEO_ID)

### Screenshots

**Defense Mode - Real-time Detection**
```
[Screenshot: Code with red underlines showing vulnerabilities]
```

**Offense Mode - Exploit Generation**
```
[Screenshot: Right-click menu showing "Generate Exploit" option]
```

**AI Security Chat**
```
[Screenshot: Chat panel with security Q&A]
```

**Attack Path Visualization**
```
[Screenshot: Graph showing attack chain]
```

---

## 🔥 What Makes It Unique?

### vs Traditional SAST Tools

| Feature | XeOps Guardian | SonarLint | Snyk | Others |
|---------|----------------|-----------|------|---------|
| **Real-time detection** | ✅ | ✅ | ✅ | ✅ |
| **AI-powered fixes** | ✅ | ❌ | ❌ | ❌ |
| **Exploit generation** | ✅ | ❌ | ❌ | ❌ |
| **Attack path viz** | ✅ | ❌ | ❌ | ❌ |
| **Offense mode** | ✅ | ❌ | ❌ | ❌ |
| **AI chat** | ✅ | ❌ | ❌ | ❌ |
| **Bug bounty integration** | ✅ | ❌ | ❌ | ❌ |

### vs GitHub Copilot

- **Copilot**: Suggests code
- **XeOps Guardian**: **Secures code**

**Use both!** Copilot writes fast code, Guardian makes it secure.

---

## 🎯 Use Cases

### For Developers
- ✅ Learn security while coding
- ✅ Catch vulnerabilities before commit
- ✅ Ship secure code faster
- ✅ No security expertise required

### For Bug Bounty Hunters
- ✅ Find vulnerabilities in target code
- ✅ Generate PoC exploits instantly
- ✅ Submit to HackerOne/YesWeHack from VS Code
- ✅ 10x your efficiency

### For Security Teams
- ✅ Train developers on secure coding
- ✅ Enforce security standards
- ✅ Catch issues before PR review
- ✅ Reduce security technical debt

### For DevSecOps
- ✅ Shift security left
- ✅ Pre-commit security checks
- ✅ Integrate with CI/CD
- ✅ Automated security gates

---

## 📚 Documentation

### Getting Started
- **[Installation Guide](./docs/vscode-extension/installation.md)** - Step-by-step setup
- **[Quick Start](./docs/vscode-extension/quickstart.md)** - 5-minute tutorial
- **[Configuration](./docs/vscode-extension/configuration.md)** - All settings explained

### Features
- **[Defense Mode](./docs/vscode-extension/defense-mode.md)** - Vulnerability scanning
- **[Offense Mode](./docs/vscode-extension/offense-mode.md)** - Exploit generation
- **[AI Chat](./docs/vscode-extension/ai-chat.md)** - Security Q&A
- **[Attack Paths](./docs/vscode-extension/attack-paths.md)** - Visualization

### Advanced
- **[Keyboard Shortcuts](./docs/vscode-extension/shortcuts.md)** - All keybindings
- **[API Integration](./docs/vscode-extension/api.md)** - Extend functionality
- **[Troubleshooting](./docs/vscode-extension/troubleshooting.md)** - Common issues

---

## 🚀 Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Shift+X M` | Switch Defense ↔ Offense mode |
| `Ctrl+Shift+X S` | Scan current file |
| `Ctrl+Shift+X W` | Scan entire workspace |
| `Ctrl+Shift+X E` | Generate exploit (Offense mode) |
| `Ctrl+Shift+X C` | Open AI security chat |
| `Ctrl+.` | Show fix suggestions |

---

## 🤝 Community

### Get Help & Connect

- **Discord**: [Join our server](https://discord.gg/xeops) - Chat with other users
- **Twitter**: [@xeops_ai](https://twitter.com/xeops_ai) - Latest updates
- **GitHub**: [xeops-ai-public](https://github.com/xeops-sofyen/xeops-ai-public) - Issues & discussions
- **Blog**: [xeops.ai/blog](https://xeops.ai/blog) - Security tutorials

### Stay Updated

- 🔔 [GitHub Releases](https://github.com/xeops-sofyen/xeops-ai-public/releases) - New versions
- 📧 [Newsletter](https://xeops.ai/newsletter) - Monthly security tips
- 🎥 [YouTube](https://youtube.com/@xeops) - Video tutorials

---

## ⭐ Show Your Support

Love XeOps Guardian? Help us grow!

- ⭐ **Star this repo** on GitHub
- 🌟 **Rate 5 stars** on [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian)
- 🐦 **Tweet about it** (tag [@xeops_ai](https://twitter.com/xeops_ai))
- 📝 **Write a review** or blog post
- 🔗 **Share with your team**

---

## 🐛 Reporting Issues

Found a bug or have a feature request?

1. **Check** [existing issues](https://github.com/xeops-sofyen/xeops-ai-public/issues)
2. **Open** a new issue with:
   - Steps to reproduce
   - Expected vs actual behavior
   - VS Code version
   - Extension version
3. **Include** VS Code extension logs (Help → Toggle Developer Tools → Console)

We respond to all issues within 24 hours!

---

## 🔐 Privacy & Security

### Your Code is Safe

- ✅ **Code stays local** - Only metadata sent to API
- ✅ **No code storage** - Nothing saved on our servers
- ✅ **TLS encryption** - All API calls encrypted
- ✅ **GDPR compliant** - Data hosted in EU
- ✅ **SOC 2 certified** - Enterprise security

### What We Collect

**Sent to API:**
- File type/language
- Vulnerability patterns found
- Code snippets (only vulnerable lines, not entire files)

**NOT sent:**
- Your complete source code
- Credentials/secrets
- Business logic

**[Read Full Privacy Policy](https://xeops.ai/privacy)**

---

## 🏆 Testimonials

> "XeOps Guardian caught 3 critical SQLi vulnerabilities before I even committed. Saved us from a potential data breach."
>
> **— Senior Developer, FinTech Startup**

> "As a bug bounty hunter, this extension 10x'd my productivity. I find vulns while browsing code, not after running scans."
>
> **— Top 100 HackerOne Hunter**

> "Finally, a security tool that doesn't slow me down. Real-time feedback while coding is a game-changer."
>
> **— Lead Security Engineer, Fortune 500**

---

## 🎓 Learning Resources

### Video Tutorials

1. **[Getting Started](https://youtube.com/watch?v=TUTORIAL_1)** (5 min)
2. **[Defense Mode Deep Dive](https://youtube.com/watch?v=TUTORIAL_2)** (15 min)
3. **[Offensive Testing Guide](https://youtube.com/watch?v=TUTORIAL_3)** (20 min)
4. **[Bug Bounty Workflow](https://youtube.com/watch?v=TUTORIAL_4)** (10 min)

### Blog Posts

- **[Ship Secure Code Faster with XeOps Guardian](https://xeops.ai/blog/vscode-extension-launch)**
- **[From Defense to Offense: Two Modes Explained](https://xeops.ai/blog/defense-offense-modes)**
- **[10 Security Bugs XeOps Catches That Others Miss](https://xeops.ai/blog/unique-detections)**

---

## 📊 Supported Languages

<div align="center">

| Language | Detection | Exploit Gen | Status |
|----------|-----------|-------------|--------|
| JavaScript/TypeScript | ✅ | ✅ | Excellent |
| Python | ✅ | ✅ | Excellent |
| Java | ✅ | ✅ | Good |
| PHP | ✅ | ✅ | Good |
| Go | ✅ | 🟡 | Beta |
| Ruby | ✅ | 🟡 | Beta |
| C# | ✅ | 🟡 | Beta |

**+10 more languages in development**

</div>

---

## 🔄 Roadmap

### Recently Shipped ✅
- Real-time vulnerability detection
- AI-powered fixes
- Attack path visualization
- Multi-model AI support

### Coming Soon 🚀
- [ ] Language Server Protocol (LSP) for better performance
- [ ] Pre-commit hooks integration
- [ ] Team collaboration features
- [ ] Custom rulesets
- [ ] IDE support (IntelliJ, WebStorm)

**[Vote on features](https://github.com/xeops-sofyen/xeops-ai-public/discussions/categories/feature-requests)**

---

## 💬 FAQ

### Q: Is my code sent to your servers?

**A**: No. Only metadata and vulnerable code snippets (not entire files) are analyzed. Your complete source code never leaves your machine.

### Q: How many scans do I get for free?

**A**: 10 scans/month on the free plan. Upgrade to Pro for unlimited scans.

### Q: Does it work offline?

**A**: No. XeOps Guardian requires internet connection to access our AI models. However, we're working on a local mode.

### Q: Can I use it for bug bounty hunting?

**A**: Absolutely! Offense mode is designed for security researchers. Generate exploits, submit to platforms directly from VS Code.

### Q: What about open-source projects?

**A**: Contact us at opensource@xeops.ai for free Pro licenses for OSS maintainers.

**[More Questions](./FAQ.md)**

---

## 🌍 Supported Platforms

- ✅ Windows 10/11
- ✅ macOS 10.15+
- ✅ Linux (Ubuntu, Debian, Fedora)
- ✅ WSL2
- ✅ Remote SSH
- ✅ Dev Containers

---

## 🔗 Integrations

### Bug Bounty Platforms
- ✅ HackerOne
- ✅ YesWeHack
- ✅ Bugcrowd
- ✅ Intigriti

### Issue Trackers
- ✅ GitHub Issues
- ✅ Jira
- ✅ Linear
- ✅ Slack

### CI/CD
- ✅ GitHub Actions
- ✅ GitLab CI
- ✅ Jenkins
- ✅ CircleCI

---

## 📞 Support

### Free Plan
- 📧 Email support (48h response)
- 📚 Documentation & guides
- 💬 Community Discord

### Pro Plan
- 📧 Priority email (24h response)
- 💬 Live chat support
- 🎯 Dedicated Slack channel

### Enterprise
- 📞 Phone support
- 👤 Dedicated account manager
- ⏱️ 4-hour SLA
- 🔧 Custom integrations

**[Contact Support](mailto:support@xeops.ai)**

---

## 🎯 Call to Action

<div align="center">

### Ready to Ship Secure Code?

[![Install Extension](https://img.shields.io/badge/INSTALL_NOW-VS_Code_Marketplace-007ACC?style=for-the-badge&logo=visual-studio-code&logoColor=white&labelColor=000000)](https://marketplace.visualstudio.com/items?itemName=xeops.xeops-guardian)

**10 free scans included** · **No credit card required** · **2-minute setup**

---

### Questions?

**Chat with us**: [Discord](https://discord.gg/xeops)
**Email us**: support@xeops.ai
**Book a demo**: [calendly.com/xeops](https://calendly.com/xeops/demo)

---

Made with ❤️ by [XeOps.AI](https://xeops.ai) • Paris, France 🇫🇷

**From Defense to Offense, in One Extension**

</div>
