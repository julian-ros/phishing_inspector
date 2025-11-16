# Phishing Inspector Documentation

Welcome to the comprehensive documentation for Phishing Inspector, a multi-layered email security analysis platform that combines AI-powered detection with threat intelligence from industry-leading services.

## Documentation Structure

This documentation is organized to serve different user types and use cases:

### 📚 User Guides
Documentation for end-users at different technical levels:
- **[Getting Started Guide](./user-guides/getting-started.md)** - Quick introduction for first-time users
- **[Normal User Guide](./user-guides/normal-user-guide.md)** - Complete guide for non-technical users
- **[SOC Analyst Guide](./user-guides/soc-analyst-guide.md)** - Advanced guide for security professionals
- **[Quick Reference](./user-guides/quick-reference.md)** - Fast lookup for common tasks

### 🔧 Technical Reference
In-depth technical documentation:
- **[Technical Architecture](./technical-reference/architecture.md)** - Multi-layered analysis system design
- **[Risk Scoring Methodology](./technical-reference/risk-scoring.md)** - How risk scores are calculated
- **[External Services Integration](./technical-reference/external-services.md)** - Threat intelligence integrations
- **[Security Glossary](./technical-reference/glossary.md)** - Key terms and concepts

### 🔄 Workflows
Step-by-step processes for different scenarios:
- **[Email Client Workflows](./workflows/email-clients.md)** - Extract email source from Gmail, Outlook, etc.
- **[Mobile Device Workflows](./workflows/mobile-devices.md)** - Analyze emails on smartphones and tablets
- **[SOC Team Workflows](./workflows/soc-team-workflows.md)** - Best practices for security teams

### 🔍 Troubleshooting
Solutions to common issues:
- **[Common Issues & Solutions](./troubleshooting/common-issues.md)** - Error messages and fixes
- **[Best Practices](./troubleshooting/best-practices.md)** - Tips for accurate analysis
- **[FAQ](./troubleshooting/faq-extended.md)** - Extended frequently asked questions

### 📖 Examples
Real-world scenarios and case studies:
- **[Phishing Examples](./examples/phishing-examples.md)** - Annotated analysis of actual phishing attempts
- **[Edge Cases](./examples/edge-cases.md)** - Unusual scenarios and how they're handled

## Quick Links

### For First-Time Users
Start here: **[Getting Started Guide](./user-guides/getting-started.md)**

### For Individual Users
Learn how to analyze suspicious emails: **[Normal User Guide](./user-guides/normal-user-guide.md)**

### For Security Professionals
Advanced features and interpretation: **[SOC Analyst Guide](./user-guides/soc-analyst-guide.md)**

### Having Issues?
Check the **[Troubleshooting Guide](./troubleshooting/common-issues.md)**

## About Phishing Inspector

Phishing Inspector is a sophisticated email security analysis platform that helps individuals and security teams identify phishing attempts, spam, and malicious emails through a multi-layered detection approach.

### Key Features
- **2 Independent AI Models**: Llama 3.1 8B and Gemma 2 2B for content analysis
- **External Threat Intelligence**: Google Safe Browsing, VirusTotal, URLhaus, URLScan.io
- **Email Authentication**: SPF, DKIM, DMARC validation
- **IP Reputation**: AbuseIPDB and DNSBL checking
- **Behavioral Analysis**: Social engineering tactic detection
- **5-Dimensional Risk Scoring**: Content, URL, Header, Attachment, and Behavioral risks
- **Dual-Interface Reporting**: Simple reports for users, technical reports for analysts

### Privacy First
All analysis happens in real-time with no data storage or logging. Your privacy is our highest priority.

## Support

For questions or issues:
- Visit the main application: https://www.phishinginspector.com
- Check the [FAQ](./troubleshooting/faq-extended.md)
- Review [Common Issues](./troubleshooting/common-issues.md)

---

**Last Updated**: November 2025
**Version**: 1.0
