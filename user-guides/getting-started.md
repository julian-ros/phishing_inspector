# Getting Started with Phishing Inspector

Welcome! This guide will help you quickly start analyzing suspicious emails using Phishing Inspector's multi-layered security analysis.

## What is Phishing Inspector?

Phishing Inspector is a free email security analysis tool that combines:
- **2 AI Models** (Llama 3.1 8B and Gemma 2 2B) for content analysis
- **4+ Threat Intelligence Services** (Google Safe Browsing, VirusTotal, URLhaus, URLScan.io)
- **Email Authentication Validation** (SPF, DKIM, DMARC)
- **IP Reputation Checking** (AbuseIPDB, DNSBL)
- **Behavioral Pattern Detection** (Social engineering tactics)

All analysis happens in real-time with **zero data storage** - your privacy is guaranteed.

## Quick Start: 3 Simple Steps

### Step 1: Get Your Email Content

**Desktop (Recommended)**
Get the complete email source with headers for most accurate analysis:

**Gmail:**
1. Open the suspicious email
2. Click the three-dot menu (⋮) in top right
3. Select "Show original"
4. Copy everything in the new tab

**Outlook:**
1. Right-click the email
2. Select "View Source" or File > Properties
3. Copy the "Internet headers" and message content

**Other Clients:**
Look for "View Source", "Show Original", or "Message Source" in menus

**Mobile (Limited Analysis)**
If you can't access email headers on mobile:
1. Open the suspicious email
2. Long-press to select all text
3. Copy sender, subject, body, and all links
4. The system will automatically detect "Body-Only Mode"

> **💡 Tip**: For best results, use desktop to access complete email source with headers

### Step 2: Paste or Upload

Visit **[Phishing Inspector](https://www.phishinginspector.com)** and choose:

**Text Input (Most Common)**
- Paste complete email source into text area
- Supports both desktop (with headers) and mobile (body-only)
- System auto-detects content type

**EML File Upload**
- Upload .eml files exported from email clients
- Contains complete headers and content
- Best for repeated analysis or archival

### Step 3: Analyze & Review

1. Click "Analyze" button
2. Wait 10-20 seconds while system checks:
   - 2 AI models analyze content
   - URLs verified against 4 threat databases
   - Email authentication checked (if headers available)
   - IP reputation verified
   - Behavioral patterns detected
3. View your report with verdict and risk score

## Understanding Your Results

### Verdicts Explained

**🔴 PHISHING (Risk 70-100)**
High-confidence phishing attempt. **Do not click links or reply.**
- Action: Delete immediately and report to IT security

**🟠 SUSPICIOUS (Risk 40-69)**
Concerning indicators detected, but not definitive.
- Action: Verify sender through alternative channels before taking action

**🟡 SPAM (Risk 60+, Spam Indicators)**
Unsolicited bulk mail, potentially misleading.
- Action: Safe to delete without concern

**🟢 LEGITIMATE (Risk 0-39)**
Email appears genuine based on all analysis layers.
- Action: Still verify unexpected requests through official channels

### Two Report Types

**Simple Report**
- Clear verdict and risk score
- Top warning signs
- Actionable recommendations
- Perfect for everyday users

**SOC Analyst Report**
- Detailed risk breakdown across 5 dimensions
- Complete IOC extraction
- External verification results
- AI model details
- MITRE ATT&CK mappings
- Best for security professionals

Switch between reports anytime using buttons at bottom.

## Analysis Modes

### Complete Analysis (Desktop with Headers)
**Checks Performed:**
- ✅ AI content analysis (2 models)
- ✅ URL verification (Google, VirusTotal, URLhaus, URLScan)
- ✅ Email authentication (SPF, DKIM, DMARC)
- ✅ IP reputation (AbuseIPDB, DNSBL)
- ✅ Domain age checking
- ✅ Behavioral analysis
- ✅ Attachment analysis

**Confidence Level:** High (75-95%)

### Body-Only Mode (Mobile/No Headers)
**Checks Performed:**
- ✅ AI content analysis (2 models)
- ✅ URL verification (Google, VirusTotal, URLhaus, URLScan)
- ✅ Domain age checking
- ✅ Behavioral analysis
- ❌ Email authentication (no headers available)
- ❌ IP reputation (no headers available)
- ❌ Routing analysis (no headers available)

**Confidence Level:** Medium (45-80%)

> **📱 Mobile Users**: The system automatically detects body-only content and adjusts analysis accordingly. You'll see a blue notice explaining the limitations.

## Common Questions

### Q: Is my data stored?
**A:** No. All analysis happens in real-time and data is immediately discarded after your report is generated. Nothing is logged or saved.

### Q: How long does analysis take?
**A:** Most analyses complete in 10-20 seconds. Body-only mode is faster (8-15 seconds) since it skips header checks.

### Q: Can I analyze emails on my phone?
**A:** Yes! While mobile devices can't easily access email headers, you can copy the email body and analyze it in Body-Only Mode. Forward the email to yourself and analyze from desktop for complete results.

### Q: What if I get an error?
**A:** Check these common issues:
- **"Insufficient content"**: Email text too short (need at least 50 characters)
- **"Body-Only Mode warning"**: Normal for mobile - limited but still valuable analysis
- **"Analysis taking too long"**: External APIs may be slow - please wait

See the [Troubleshooting Guide](../troubleshooting/common-issues.md) for more solutions.

### Q: Is the analysis 100% accurate?
**A:** No system is perfect. Our multi-layered approach provides highly accurate results, but sophisticated attackers continuously evolve. Always use professional judgment, especially for critical decisions.

## Next Steps

### For Regular Users
Learn more about interpreting results and best practices:
→ **[Normal User Guide](./normal-user-guide.md)**

### For Security Professionals
Explore advanced features and technical details:
→ **[SOC Analyst Guide](./soc-analyst-guide.md)**

### Need Email Client Help?
Step-by-step instructions for every major email client:
→ **[Email Client Workflows](../workflows/email-clients.md)**

### Having Issues?
Solutions to common problems:
→ **[Troubleshooting Guide](../troubleshooting/common-issues.md)**

## Privacy & Security

**What We DO:**
- Analyze emails in real-time
- Send URLs to threat intelligence APIs for verification
- Send IPs to reputation services (AbuseIPDB, DNSBL)
- Provide detailed security reports

**What We DON'T DO:**
- Store or log email content
- Save URLs, IPs, or any analysis data
- Track users or create profiles
- Share data with third parties (except necessary API queries)
- Require account creation or login

Your privacy and security are our highest priorities. Use Phishing Inspector with confidence.

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────────────┐
│ PHISHING INSPECTOR QUICK START                          │
├─────────────────────────────────────────────────────────┤
│ 1. GET EMAIL SOURCE                                     │
│    • Gmail: ⋮ menu → "Show original"                    │
│    • Outlook: Right-click → "View Source"               │
│    • Mobile: Copy entire email body                     │
│                                                         │
│ 2. PASTE & ANALYZE                                      │
│    • Visit phishinginspector.com                        │
│    • Paste content → Click "Analyze"                    │
│    • Wait 10-20 seconds                                 │
│                                                         │
│ 3. REVIEW VERDICT                                       │
│    • PHISHING (70-100): Delete & report                 │
│    • SUSPICIOUS (40-69): Verify first                   │
│    • SPAM (60+): Delete safely                          │
│    • LEGITIMATE (0-39): Still verify unexpected actions │
│                                                         │
│ FEATURES:                                               │
│    ✓ 2 AI Models          ✓ Google Safe Browsing       │
│    ✓ VirusTotal (70+)     ✓ URLhaus + URLScan          │
│    ✓ SPF/DKIM/DMARC       ✓ IP Reputation              │
│    ✓ Zero Data Storage    ✓ 100% Private               │
└─────────────────────────────────────────────────────────┘
```

Need help? Check the [FAQ](../troubleshooting/faq-extended.md) or [Common Issues](../troubleshooting/common-issues.md) guide.

---

**Ready to analyze your first email?** Visit **[Phishing Inspector](https://www.phishinginspector.com)** now!
