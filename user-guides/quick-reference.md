# Quick Reference Guide

Fast lookup reference for Phishing Inspector users. Print or bookmark this page for quick access during email analysis.

## Quick Start (30 Seconds)

```
1. Get email → Gmail: ⋮ menu → "Show original" | Outlook: Right-click → "View Source"
2. Paste → Visit phishinginspector.com → Paste email source
3. Analyze → Click "Analyze" → Wait 10-20 seconds
4. Act → Follow verdict recommendation
```

## Verdict Quick Reference

| Verdict | Risk Score | Meaning | Action |
|---------|------------|---------|--------|
| 🔴 **PHISHING** | 70-100 | High-confidence threat | **DELETE** immediately, report to IT |
| 🟠 **SUSPICIOUS** | 40-69 | Concerning indicators | **VERIFY** through official channels first |
| 🟡 **SPAM** | 60+ (spam) | Unwanted bulk mail | **DELETE** safely, mark as spam |
| 🟢 **LEGITIMATE** | 0-39 | Appears genuine | Safe to interact, but verify unexpected requests |

## Email Client Commands

### Desktop

**Gmail:**
```
Three-dot menu (⋮) → "Show original" → Copy all
```

**Outlook Desktop:**
```
Right-click email → "View Source" OR File → Properties → Copy headers
```

**Outlook Web:**
```
Three-dot menu (...) → View → "View message source" → Copy all
```

**Apple Mail:**
```
View → Message → Raw Source (Option+Cmd+U) → Copy all
```

**Yahoo Mail:**
```
More (...) → "View Raw Message" → Copy all
```

**Thunderbird:**
```
View → Message Source (Ctrl+U / Cmd+U) → Copy all
```

### Mobile

**iPhone/Android:**
```
Long-press email → Select all → Copy
Include: Sender, Subject, Body, Links
System auto-detects "Body-Only Mode"
```

## Risk Dimensions

| Dimension | Weight | What It Checks |
|-----------|--------|----------------|
| **Content** | 35% | AI models (Llama 3.1, Gemma 2), phishing patterns, social engineering |
| **URL** | 30% | Google Safe Browsing, VirusTotal, URLhaus, URLScan.io |
| **Header** | 20% | SPF/DKIM/DMARC, IP reputation, routing analysis |
| **Attachment** | 10% | File types, hashes, malware indicators |
| **Behavioral** | 5% | Urgency, authority, fear tactics |

## Warning Signs Checklist

### 🚩 Red Flags (Immediate Delete)

- [ ] Malicious URL confirmed by Google/VirusTotal
- [ ] SPF/DKIM/DMARC all failed
- [ ] IP blacklisted on multiple DNSBLs
- [ ] Executable attachment (.exe, .scr, .bat)
- [ ] Requests password/credit card via email
- [ ] Extreme urgency ("Account suspended in 1 hour")

### ⚠️ Yellow Flags (Verify First)

- [ ] Newly registered domain (<180 days)
- [ ] Generic greeting ("Dear Customer")
- [ ] Sender address doesn't match company
- [ ] Unexpected request from known contact
- [ ] URL doesn't match displayed text
- [ ] Minor spelling/grammar errors

### ✅ Green Flags (Likely Safe)

- [ ] SPF, DKIM, DMARC all passed
- [ ] All URLs verified clean (Google, VirusTotal)
- [ ] Personalized greeting with your name
- [ ] Expected email (you initiated)
- [ ] No urgency or threats
- [ ] Clean IP reputation

## External Verification

| Service | Purpose | Trustworthiness |
|---------|---------|-----------------|
| **Google Safe Browsing** | Phishing & malware detection | ⭐⭐⭐⭐⭐ Highest (billions of users) |
| **VirusTotal** | 70+ antivirus engines | ⭐⭐⭐⭐⭐ Very High (multi-engine) |
| **URLhaus** | Malware distribution database | ⭐⭐⭐⭐ High (specialized) |
| **URLScan.io** | Live URL scanning | ⭐⭐⭐⭐ High (detailed analysis) |
| **AbuseIPDB** | IP abuse reports | ⭐⭐⭐⭐ High (community-driven) |
| **DNSBL** | Spam blacklists | ⭐⭐⭐⭐ High (Spamhaus, SpamCop) |

## Confidence Levels

| Confidence | Interpretation | Recommended Action |
|------------|----------------|-------------------|
| **90-95%** | Very high certainty | Trust verdict, act immediately |
| **75-89%** | High certainty | Safe for most decisions |
| **60-74%** | Medium certainty | Manual review for critical decisions |
| **45-59%** | Low certainty | Requires analyst judgment |

**Confidence Adjusted By:**
- ✅ Perfect AI consensus: +10%
- ✅ External verification confirmed: +10%
- ❌ Body-only mode (mobile): -15%
- ❌ Missing headers: -12%
- ❌ Mixed signals: -10%

## Analysis Modes

### Complete Analysis (Desktop)
**Data Available:** ✅ All
**Checks:** AI models, URLs, Authentication, IP, Domains, Attachments, Behavioral
**Confidence:** High (75-95%)
**Time:** 10-20 seconds

### Body-Only Mode (Mobile)
**Data Available:** ❌ No headers
**Checks:** AI models, URLs, Domains, Behavioral
**Skipped:** Authentication, IP reputation, Routing
**Confidence:** Medium (45-80%, -15% penalty)
**Time:** 8-15 seconds

## Common Errors

| Error | Cause | Solution |
|-------|-------|----------|
| "Insufficient content" | Text too short (<50 chars) | Copy complete email including headers |
| "Body-Only Mode" warning | Mobile / no headers | Normal for mobile - use desktop for full analysis |
| "Analysis taking too long" | External API delays | Wait - system continues processing |
| "Service not configured" | Optional API unavailable | Analysis continues with other services |

## Email Authentication

### SPF (Sender Policy Framework)
- ✅ **PASS**: Sender IP authorized by domain
- ❌ **FAIL**: Strong spoofing indicator
- ⚠️ **SOFTFAIL/NEUTRAL**: Questionable authorization

### DKIM (DomainKeys Identified Mail)
- ✅ **PASS**: Email signature valid, not modified
- ❌ **FAIL**: Signature invalid or email forged
- ⚠️ **NONE**: No signature (concerning for established senders)

### DMARC (Domain-based Message Authentication)
- ✅ **PASS**: Authenticated per domain policy
- ❌ **FAIL**: Domain owner explicitly rejects this email
- ⚠️ **NONE**: No policy (domain not protected)

## MITRE ATT&CK Quick Codes

| Technique | Name | Description |
|-----------|------|-------------|
| **T1566.002** | Phishing: Spearphishing Link | Malicious links to steal credentials |
| **T1566.001** | Phishing: Spearphishing Attachment | Malicious attachments for code execution |
| **T1598.003** | Phishing for Information | Gathering personal/financial info |
| **T1534** | Internal Spearphishing | Compromised account sending phishing |

## Report Sections (SOC Analyst)

### Tabs Overview
1. **IOCs** → URLs, IPs, Domains, Emails, Keywords, Attachments
2. **External APIs** → Detailed verification results (Google, VirusTotal, etc.)
3. **Models** → AI analysis from Llama 3.1 & Gemma 2
4. **Headers** → SPF/DKIM/DMARC, IP reputation, routing path
5. **MITRE** → ATT&CK technique mappings
6. **Actions** → Recommendations and detailed findings

## IOC Priorities

### Immediate Block (Critical)
1. URLs confirmed malicious by Google Safe Browsing
2. IPs with 75%+ abuse score on AbuseIPDB
3. Domains on URLhaus malware list
4. IPs blacklisted on Spamhaus

### Monitor/Investigate
1. Newly registered domains (<90 days)
2. URLs flagged by 1-2 VirusTotal engines
3. IPs with 25-74% abuse score
4. Soft-fail SPF results

## Response Actions

### For PHISHING Verdict

**Immediate:**
1. ❌ Do not click links or download attachments
2. 🚫 Do not reply or provide information
3. 🔒 Report to IT security team
4. 🗑️ Delete email after reporting

**If Clicked:**
1. 🔐 Change passwords immediately
2. 📱 Enable 2FA on affected accounts
3. 👁️ Monitor for suspicious activity
4. 📞 Contact bank if financial info shared
5. 🛡️ Run antivirus scan
6. 📧 Report: reportphishing@apwg.org or FBI IC3

### For SUSPICIOUS Verdict

**Recommended:**
1. ⏸️ Do not click yet
2. ✅ Verify sender through official channels (call company, login directly)
3. 🔍 Check SOC Analyst Report for details
4. ❓ When in doubt, don't click

### For LEGITIMATE Verdict

**Best Practice:**
1. ✅ Likely safe to interact
2. ⚠️ Still verify unexpected financial requests
3. 🚫 Never provide passwords via email (even if email is legitimate)
4. 🔗 Type important URLs manually instead of clicking

## Keyboard Shortcuts (Web Interface)

Currently no keyboard shortcuts - manual navigation required.

## Common Phishing Tactics

| Tactic | Example | Detection |
|--------|---------|-----------|
| **Urgency** | "Account closes in 24h" | Behavioral analysis flags |
| **Authority** | Impersonating CEO/IRS | Brand detection, authentication fails |
| **Fear** | "Security breach detected" | Social engineering scoring |
| **Greed** | "$1M lottery win" | Content analysis patterns |
| **Trust** | Compromised friend | Internal spearphishing detection |

## Best Practices Summary

### ✅ DO:
- Use complete email source from desktop for highest accuracy
- Read full report, not just verdict
- Verify unexpected requests through official channels
- Enable 2FA on all important accounts
- Report confirmed phishing to IT/email provider
- Forward suspicious email to desktop if analyzing from mobile

### ❌ DON'T:
- Click links to "test if safe" (use Phishing Inspector first)
- Trust screenshots or forwarded emails (lose header data)
- Ignore low confidence scores
- Provide passwords/credit cards via email (EVER)
- Assume 100% accuracy (always use judgment)
- Share sensitive info even if email marked legitimate

## Privacy Reminder

**What Phishing Inspector DOES NOT do:**
- ❌ Store or log email content
- ❌ Save URLs, IPs, or analysis results
- ❌ Track users or create profiles
- ❌ Share data (except necessary API queries)
- ❌ Require accounts or login

**Your analysis is private and secure.**

## Quick Links

- **Main App**: [phishinginspector.com](https://www.phishinginspector.com)
- **Full User Guide**: [Normal User Guide](./normal-user-guide.md)
- **Technical Guide**: [SOC Analyst Guide](./soc-analyst-guide.md)
- **Troubleshooting**: [Common Issues](../troubleshooting/common-issues.md)
- **Report Phishing**: [reportphishing@apwg.org](mailto:reportphishing@apwg.org)
- **FBI IC3**: [ic3.gov](https://www.ic3.gov)

---

## Printable Checklist

Before clicking any email link:

```
□ Email analyzed with Phishing Inspector?
□ Verdict is LEGITIMATE or risk score < 40?
□ Confidence score > 75%?
□ Sender address looks correct?
□ No urgency or threats?
□ Personalized with my name?
□ Expected this email?
□ No requests for passwords/credit cards?
□ Verified unexpected requests through official channels?

If ALL checked: Probably safe
If ANY unchecked: VERIFY FIRST
```

---

**Questions?** See [FAQ](../troubleshooting/faq-extended.md) | **Issues?** See [Troubleshooting](../troubleshooting/common-issues.md)

**Print this page for quick reference during email analysis!**
