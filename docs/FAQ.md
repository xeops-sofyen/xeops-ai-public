# Frequently Asked Questions (FAQ)

## General Questions

### What is XeOps Guardian?
XeOps Guardian is a VS Code extension that provides AI-powered vulnerability scanning and ethical hacking capabilities for developers and security teams.

### Is XeOps Guardian free?
The VS Code extension itself is free and open source. However, to access the AI-powered features, exploit generation, and advanced scanning capabilities, you need a subscription at [xeops.ai](https://xeops.ai).

### What's the difference between the free and paid versions?
- **Free (Extension only):** Basic local scanning, syntax highlighting
- **Paid (With API):** AI vulnerability analysis, exploit generation, compliance reports, cloud scanning

### Which programming languages are supported?
Currently supported:
- JavaScript/TypeScript
- Python
- Java
- PHP

More languages coming soon!

## Installation & Setup

### How do I install the extension?
```bash
code --install-extension xeops.xeops-guardian
```
Or search "XeOps Guardian" in the VS Code marketplace.

### How do I get an API key?
1. Sign up at [xeops.ai](https://xeops.ai)
2. Choose a subscription plan
3. Get your API key from the dashboard
4. Configure it in VS Code settings

### The extension is not working, what should I do?
1. Check VS Code version (minimum 1.74.0)
2. Verify your API key is configured correctly
3. Check the output panel: View > Output > XeOps Guardian
4. Restart VS Code
5. If issues persist, contact support@xeops.ai

## Features

### What vulnerabilities can XeOps detect?
- OWASP Top 10 vulnerabilities
- SQL Injection
- XSS (Cross-Site Scripting)
- Command Injection
- Path Traversal
- Insecure Deserialization
- And 20+ more vulnerability types

### Can XeOps generate real exploits?
Yes, with a paid subscription, XeOps can generate verified proof-of-concept (PoC) exploits for educational and authorized testing purposes only.

### Is it legal to use XeOps Guardian?
Yes, when used for:
- Authorized security testing
- Bug bounty programs
- Educational purposes
- Testing your own applications

Never use it for unauthorized access or malicious purposes.

## Pricing & Licensing

### What are the pricing plans?
- **Starter:** €49/month - 100 scans, 5 members
- **Professional:** €149/month - 500 scans, 20 members
- **Enterprise:** €499/month - Unlimited scans, white-label

See full details at [xeops.ai/pricing](https://xeops.ai/pricing)

### Is the extension open source?
Yes, the VS Code extension is open source under MIT license. The backend AI and API services are proprietary.

### Can I self-host XeOps?
The extension can run locally, but the AI services require our cloud infrastructure. Enterprise customers can discuss on-premise options.

## Technical

### Does XeOps send my code to the cloud?
Only when you explicitly request AI analysis or exploit generation. Local scanning happens entirely on your machine.

### Is my code secure?
- All communications are encrypted (TLS 1.3)
- Code is not stored on our servers
- We comply with GDPR and data protection regulations
- Enterprise plans include additional security guarantees

### What are the system requirements?
- VS Code 1.74.0 or higher
- Node.js 16+ (for development)
- 2GB RAM minimum
- Internet connection (for AI features)

## Troubleshooting

### Extension doesn't detect vulnerabilities
- Ensure file is saved
- Check file type is supported
- Verify real-time scanning is enabled
- Try manual scan: Ctrl+Shift+P → "XeOps: Scan Current File"

### API errors
- Verify API key in settings
- Check internet connection
- Ensure subscription is active
- Check rate limits (see dashboard)

### Performance issues
- Disable real-time scanning for large files
- Exclude folders in settings
- Use manual scanning instead of automatic

## Contributing

### How can I contribute?
See our [Contributing Guide](../CONTRIBUTING.md). We welcome:
- Bug reports
- Feature requests
- Code contributions
- Documentation improvements
- Translations

### Where do I report bugs?
- Security issues: security@xeops.ai (private)
- Regular bugs: [GitHub Issues](https://github.com/xeops-sofyen/xeops-ai-public/issues)

### Can I add support for a new language?
Yes! Please open an issue first to discuss, then submit a PR with:
- Language grammar definitions
- Vulnerability patterns
- Test cases

## Support

### How do I get help?
- Documentation: This FAQ and docs/
- Email: support@xeops.ai
- Discord: [Join our server](https://discord.gg/xeops)
- GitHub: [Discussions](https://github.com/xeops-sofyen/xeops-ai-public/discussions)

### Response times?
- Starter: 48 hours
- Professional: 24 hours (priority)
- Enterprise: 4 hours SLA

### Is there a refund policy?
Yes, 14-day money-back guarantee for first-time subscribers.

## Privacy & Compliance

### Is XeOps GDPR compliant?
Yes, we are fully GDPR compliant. See our privacy policy at xeops.ai/privacy

### Do you store scan results?
- Free/Starter: No storage
- Professional: 30-day retention (optional)
- Enterprise: Customizable retention

### Can I use XeOps for compliance reporting?
Yes, Professional and Enterprise plans include:
- ISO 27001 reports
- SOC 2 reports
- PCI-DSS compliance checks

## Roadmap

### What features are coming next?
- More language support (Go, Rust, C++)
- IDE integrations (IntelliJ, PyCharm)
- CI/CD pipeline integration
- Mobile app scanning
- Web3/Smart contract analysis

### How can I request a feature?
Open a feature request on [GitHub](https://github.com/xeops-sofyen/xeops-ai-public/issues/new?template=feature_request.md)

---

**Still have questions?** Contact us at support@xeops.ai