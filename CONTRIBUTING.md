# Contributing to XeOps Guardian

First off, thank you for considering contributing to XeOps Guardian! 🎉

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Community](#community)

## 📜 Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct:

- Be respectful and inclusive
- Welcome newcomers and help them get started
- Focus on constructive criticism
- Accept feedback gracefully
- Put the community first

## 🚀 Getting Started

### Prerequisites

- Node.js 16+
- VS Code 1.74+
- Git

### Understanding the Architecture

```
Extension (Open Source)          Backend (Proprietary)
    │                                   │
    ├── UI Components                   ├── AI Engine
    ├── VS Code Integration             ├── Exploit Generation
    ├── API Client           ←→         ├── API Services
    └── Local Scanning                  └── Cloud Infrastructure
```

> **Note:** This repository contains only the extension code. The backend services are proprietary.

## 🤝 How Can I Contribute?

### Reporting Bugs

- Check existing issues first
- Use the bug report template
- Include reproduction steps
- Add screenshots if applicable

### Suggesting Features

- Check the roadmap first
- Use the feature request template
- Explain the use case clearly
- Consider implementation details

### Code Contributions

Areas where we especially welcome contributions:

- 🎨 UI/UX improvements
- 🐛 Bug fixes
- 📚 Documentation
- 🌍 Translations
- ⚡ Performance optimizations
- 🧪 Tests

## 💻 Development Setup

1. **Fork and Clone**
```bash
git clone https://github.com/YOUR-USERNAME/xeops-ai-public.git
cd xeops-ai-public/extensions/xeops-guardian
```

2. **Install Dependencies**
```bash
npm install
```

3. **Development Mode**
```bash
# Watch mode for development
npm run watch

# Or compile once
npm run compile
```

4. **Run Extension**
- Open VS Code
- Press `F5` to open a new VS Code window with the extension loaded
- Open a test file to see the extension in action

5. **Run Tests**
```bash
npm test
```

## 🔄 Pull Request Process

### Before Creating a PR

1. **Create a Feature Branch**
```bash
git checkout -b feature/your-feature-name
```

2. **Make Your Changes**
- Write clean, documented code
- Add tests if applicable
- Update documentation

3. **Test Your Changes**
```bash
npm run lint
npm test
npm run compile
```

### Creating the PR

1. **Commit Your Changes**
```bash
git add .
git commit -m "feat: add amazing feature"
```

We use [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation
- `style:` Code style changes
- `refactor:` Code refactoring
- `perf:` Performance improvements
- `test:` Test changes
- `chore:` Build process or auxiliary tool changes

2. **Push to Your Fork**
```bash
git push origin feature/your-feature-name
```

3. **Open a Pull Request**
- Use a clear title and description
- Reference any related issues
- Add screenshots for UI changes
- Request review from maintainers

### After Creating the PR

- Respond to feedback promptly
- Make requested changes
- Keep the PR updated with main branch
- Be patient - reviews take time

## 📏 Coding Standards

### TypeScript/JavaScript

- Use TypeScript for new code
- Follow existing code style
- Use meaningful variable names
- Add JSDoc comments for functions

```typescript
/**
 * Scans a file for vulnerabilities
 * @param filePath - Path to the file to scan
 * @returns Array of detected vulnerabilities
 */
async function scanFile(filePath: string): Promise<Vulnerability[]> {
  // Implementation
}
```

### File Structure

```
src/
├── commands/        # VS Code commands
├── providers/       # Data providers
├── views/          # Webview components
├── utils/          # Utility functions
└── extension.ts    # Main entry point
```

### Testing

- Write tests for new features
- Maintain test coverage above 70%
- Use descriptive test names

```typescript
describe('VulnerabilityScanner', () => {
  it('should detect SQL injection in query string', async () => {
    // Test implementation
  });
});
```

## 🎯 What We're Looking For

### High Priority

- Performance improvements for large files
- Better error messages and handling
- More language support
- UI/UX enhancements

### Good First Issues

Look for issues labeled `good first issue` - these are perfect for newcomers!

## ⚠️ What NOT to Include

Please do NOT include:

- API keys or secrets
- Proprietary backend code
- Exploit generation logic
- Customer data or examples
- Security vulnerabilities (report privately)

## 🔐 Security

For security vulnerabilities, please email security@xeops.ai instead of creating a public issue.

## 📝 Documentation

- Update README.md if needed
- Add JSDoc comments
- Update CHANGELOG.md
- Create examples if applicable

## 🤔 Questions?

- Check our [FAQ](docs/FAQ.md)
- Join our [Discord](https://discord.gg/xeops)
- Email: support@xeops.ai

## 📄 License

By contributing, you agree that your contributions will be licensed under the MIT License.

## 🙏 Recognition

Contributors will be:
- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Given credit in the extension

## 🎉 Thank You!

Every contribution, no matter how small, helps make XeOps Guardian better. We appreciate your time and effort!

---

**Ready to contribute?** Check out the [open issues](https://github.com/xeops-sofyen/xeops-ai-public/issues) and get started!