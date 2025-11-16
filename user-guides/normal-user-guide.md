# Normal User Guide

This guide is designed for everyday users who want to check suspicious emails without needing technical security expertise. Learn how to use Phishing Inspector to protect yourself from phishing attacks and email scams.

## Table of Contents
- [Why Use Phishing Inspector](#why-use-phishing-inspector)
- [Step-by-Step Analysis](#step-by-step-analysis)
- [Understanding Your Report](#understanding-your-report)
- [What to Do Based on Verdict](#what-to-do-based-on-verdict)
- [Common Warning Signs](#common-warning-signs)
- [Best Practices](#best-practices)
- [Real-World Examples](#real-world-examples)

## Why Use Phishing Inspector

### What is Phishing?
Phishing is when criminals send fake emails pretending to be from legitimate companies (like your bank, Amazon, PayPal, or government agencies) to trick you into:
- Giving them your passwords or credit card numbers
- Clicking malicious links that install malware
- Sending money or gift cards
- Sharing personal information

### Why It's Dangerous
- **90%+ of cyberattacks start with phishing emails**
- Costs individuals and businesses billions annually
- Can lead to identity theft, financial loss, and data breaches
- Attacks are becoming increasingly sophisticated and hard to spot

### How Phishing Inspector Helps
Instead of relying on just one detection method, Phishing Inspector uses **multiple independent security layers**:

1. **2 AI Models** analyze email content for phishing patterns
2. **Google Safe Browsing** checks if links are on Google's threat list (used by Chrome, Firefox, Safari)
3. **VirusTotal** scans URLs with 70+ antivirus engines
4. **URLhaus** checks malware distribution databases
5. **URLScan.io** provides detailed threat intelligence
6. **Email Authentication** validates if sender is who they claim to be (SPF, DKIM, DMARC)
7. **IP Reputation** checks if sending server is known for abuse
8. **Behavioral Analysis** detects social engineering tactics


## Step-by-Step Analysis

### Desktop Analysis (Recommended)

#### Step 1: Open the Suspicious Email
Don't click any links or download attachments yet!

#### Step 2: Get the Email Source

**Gmail:**
1. Click the **three-dot menu** (⋮) in the top right corner
2. Select **"Show original"**
3. A new tab opens - click **"Copy to clipboard"** or press Ctrl+A (Cmd+A on Mac) and copy


**Outlook Desktop:**
1. Right-click the email in your inbox
2. Select **"View Source"** or go to **File > Properties**
3. Copy everything from the "Internet headers" section


**Outlook Web:**
1. Click the **three-dot menu** (...) at the top
2. Select **"View" > "View message source"**
3. Copy all the text

**Apple Mail:**
1. Click **View** in menu bar
2. Select **Message > Raw Source** (or press Option+Cmd+U)
3. Copy everything

**Yahoo Mail:**
1. Click **"More"** (...)
2. Select **"View Raw Message"**
3. Copy all content

#### Step 3: Paste Into Phishing Inspector
1. Go to **[phishinginspector.com](https://www.phishinginspector.com)**
2. Make sure the **"Text"** tab is selected
3. Paste the email source you copied
4. Click **"Analyze Text"** button


#### Step 4: Wait for Analysis
The system will analyze your email through all security layers (10-20 seconds):
- Parsing email structure
- Running AI analysis
- Verifying URLs with threat intelligence
- Checking email authentication
- Analyzing behavioral patterns


### Mobile Analysis (Limited)

If you're on your phone and can't access email headers:

#### Step 1: Open the Suspicious Email
Don't tap any links!

#### Step 2: Copy Email Content
1. Long-press on the email text
2. Drag selection handles to select **everything** (sender, subject, body, links)
3. Tap **"Copy"** or **"Select All"** then **"Copy"**

Try to include:
- Sender email address (From:)
- Subject line
- Complete email body
- All visible links

#### Step 3: Analyze in Body-Only Mode
1. Go to **[phishinginspector.com](https://www.phishinginspector.com)**
2. Paste the content you copied
3. Click **"Analyze"**
4. You'll see a blue notice: **"Mobile/Body-Only Analysis Mode"**

The system will still check:
- ✅ AI content analysis (2 models)
- ✅ URL verification (all threat databases)
- ✅ Domain age
- ✅ Behavioral patterns

But **cannot check** (due to missing headers):
- ❌ Email authentication (SPF, DKIM, DMARC)
- ❌ IP reputation
- ❌ Email routing path

> **💡 Best Practice**: For complete analysis, forward the email to yourself and analyze it from a desktop computer when possible.


## Understanding Your Report

### The Simple Report

After analysis, you'll see the **Simple Report** designed for easy understanding:


#### Key Components:

**1. Verdict Badge**
Large colored badge showing the final determination:
- 🔴 **PHISHING** (red) - Confirmed threat
- 🟠 **SUSPICIOUS** (orange) - Concerning indicators
- 🟡 **SPAM** (yellow/orange) - Unwanted mail
- 🟢 **LEGITIMATE** (green) - Appears safe

**2. Risk Score (0-100)**
Overall threat level combining all analysis layers:
- **70-100**: High risk (Phishing)
- **40-69**: Medium risk (Suspicious/Spam)
- **0-39**: Low risk (Legitimate)

**3. Executive Summary**
Plain-English explanation of findings, written by AI based on analysis results.


**4. Warning Signs Detected**
List of specific red flags found in the email:
- Malicious URLs (verified by Google, VirusTotal, etc.)
- Failed email authentication
- Urgency tactics
- Suspicious domains
- Impersonation attempts

When a URL is verified as malicious by external services like Google Safe Browsing, you'll see a **"✓ Verified by Google"** badge for high confidence.


**5. Recommendation**
Clear action steps based on verdict severity.


### Special Notices

#### Body-Only Mode Notice (Mobile)
Blue alert explaining analysis was performed without headers:

```
📱 Mobile/Body-Only Analysis Mode

Analysis performed on email body content without headers (typically from mobile devices).

Available checks: AI content analysis (2 models), URL verification (Google Safe Browsing,
VirusTotal, URLhaus, URLScan.io), Domain age, Behavioral patterns.

Unavailable checks: Email authentication (SPF, DKIM, DMARC), IP reputation, Email routing.

Confidence reduced by 15% due to missing header data. For complete analysis with highest
confidence, access email from desktop and use "Show original" or "View Source".
```

#### Newly Registered Domain Warning
Orange alert if email contains domains registered less than 180 days ago:

```
⚠️ Newly Registered Domain Detected

This email contains 1 domain registered less than 180 days ago.
Phishing attacks often use newly registered domains to avoid detection.

• suspicious-bank.com - 45 days old (Registrar: NameCheap)
```

#### Externally Verified Threats
Green alert when threats are confirmed by major security services:

```
✅ Externally Verified Threats

2 malicious URL(s) confirmed by Google Safe Browsing, a database used by billions of
people worldwide to protect against phishing and malware.
```

## What to Do Based on Verdict

### 🔴 PHISHING (Risk 70-100)

**What It Means:**
High-confidence phishing attempt designed to steal your information or money.

**Immediate Actions:**
1. ❌ **DO NOT** click any links in the email
2. ❌ **DO NOT** download any attachments
3. ❌ **DO NOT** reply or provide any information
4. ❌ **DO NOT** call phone numbers in the email
5. ✅ **Report it** to your IT security team (work) or email provider
6. ✅ **Delete the email** immediately after reporting
7. ✅ **Warn others** if the email appears to come from a compromised contact

**If You Already Clicked:**
1. **Change passwords immediately** for any accounts related to the email
2. **Enable two-factor authentication** on affected accounts
3. **Monitor accounts** for suspicious activity
4. **Contact your bank** if you provided financial information
5. **Run antivirus scan** if you downloaded attachments
6. **Report to authorities**: [reportphishing@apwg.org](mailto:reportphishing@apwg.org) or [FBI IC3](https://www.ic3.gov)

### 🟠 SUSPICIOUS (Risk 40-69)

**What It Means:**
Email shows concerning indicators but lacks definitive proof of malicious intent. Could be:
- Legitimate email with unusual characteristics
- Phishing attempt using sophisticated evasion techniques
- Compromised legitimate account
- Poorly configured legitimate email server

**Recommended Actions:**
1. ⚠️ **DO NOT** click links or download attachments yet
2. ✅ **Verify sender** through alternative channels:
   - Call the company using official phone number from their website (not from email)
   - Log into your account directly (type URL yourself, don't click email link)
   - Contact the person who supposedly sent it using a different method
3. ✅ **Look for red flags**:
   - Generic greeting instead of your name
   - Urgent or threatening language
   - Request for sensitive information
   - Unusual sender address
4. ✅ **Check the SOC Analyst Report** for detailed findings
5. ✅ **When in doubt, don't click** - legitimate companies will not mind you verifying

### 🟡 SPAM (Risk 60+, Spam Indicators)

**What It Means:**
Unsolicited bulk email, often containing:
- Misleading advertising
- Low-quality products
- "Too good to be true" offers
- Newsletter you didn't sign up for

**Recommended Actions:**
1. ✅ **Delete without concern** - not dangerous, just annoying
2. ✅ **Mark as spam** in your email client to improve filtering
3. ✅ **Unsubscribe** if there's a legitimate unsubscribe link (check if sender looks real)
4. ❌ **Don't engage** with obvious scam offers

### 🟢 LEGITIMATE (Risk 0-39)

**What It Means:**
Email appears genuine based on all analysis layers:
- AI models found no phishing patterns
- URLs verified as safe by threat intelligence
- Email authentication passed (if headers available)
- No suspicious behavioral patterns
- Sender IP has good reputation

**Recommended Actions:**
1. ✅ Email is likely safe to interact with
2. ⚠️ **STILL verify unexpected requests**:
   - Request for money, even from known contacts
   - Unusual payment changes (bank account, wire transfer)
   - Requests for passwords or sensitive information (legitimate companies never ask)
   - Urgent action required on financial accounts
3. ✅ **Use common sense** - even legitimate emails can be from compromised accounts
4. ✅ **Verify through official channels** for important financial or personal decisions

> **Important**: No analysis is 100% perfect. Sophisticated attackers continuously evolve their techniques. Always use professional judgment.

## Common Warning Signs

### What Phishing Inspector Looks For

**1. Malicious URLs**
- Links verified as threats by Google Safe Browsing, VirusTotal, URLhaus, or URLScan.io
- URLs that don't match displayed text (e.g., shows "paypal.com" but links to "paypa1-verify.com")
- Shortened URLs (bit.ly, tinyurl) used to hide destination
- Suspicious domains with typos (g00gle.com, micros0ft.com)
- Newly registered domains (less than 180 days old)

**2. Failed Email Authentication**
- SPF fail: Sender is not authorized by domain owner
- DKIM fail: Email was modified in transit or forged
- DMARC fail: Failed authentication and domain has strict policy

**3. Social Engineering Tactics**
- **Urgency**: "Account will be closed in 24 hours!"
- **Authority**: Impersonating CEO, IRS, police
- **Fear**: "Your account has been compromised"
- **Curiosity**: "You have a package waiting"
- **Greed**: "You've won $1,000,000"
- **Trust exploitation**: Impersonating known brands or contacts

**4. Suspicious Content Patterns**
- Requests for passwords, credit cards, SSN
- Generic greetings ("Dear Customer" instead of your name)
- Poor grammar and spelling (not always present in modern phishing)
- Mismatched sender name and email address
- Suspicious attachments (.exe, .zip, .scr, macro-enabled documents)

**5. IP Reputation Issues**
- Sending IP flagged by AbuseIPDB (abuse reports from network admins)
- Listed on DNS blacklists (Spamhaus, SpamCop, Barracuda, SORBS)
- Located in country mismatched with claimed sender

## Best Practices

### Before Analyzing

**✅ DO:**
- Copy complete email source with headers from desktop (Gmail "Show original", Outlook "View Source")
- Include sender, subject, body, and all links when copying from mobile
- Analyze emails before clicking links or downloading attachments
- Use common sense and be skeptical of unexpected requests

**❌ DON'T:**
- Take screenshots instead of copying text (can't be analyzed)
- Forward emails instead of using "Show original" (loses headers)
- Edit or shorten content before analysis (reduces accuracy)
- Click links to "see if they're safe" (verification is automated)

### During Analysis

**✅ DO:**
- Wait for complete analysis (10-20 seconds)
- Read the entire report, not just the verdict
- Check external verification results (Google, VirusTotal badges)
- Note confidence score (higher = more certain)

**❌ DON'T:**
- Stop analysis early
- Ignore warnings about body-only mode
- Dismiss low confidence scores

### After Analysis

**✅ DO:**
- Follow recommendations based on verdict
- Switch to SOC Analyst Report if you need more details
- Verify suspicious emails through alternative channels
- Report confirmed phishing to your IT team or email provider
- Share knowledge with friends and family

**❌ DON'T:**
- Assume 100% accuracy (no system is perfect)
- Click links even if marked legitimate without verifying unexpected requests
- Ignore your gut feeling (if something feels wrong, verify!)
- Share sensitive information via email, even if email looks legitimate

### General Email Security

**✅ DO:**
- Enable two-factor authentication on all important accounts
- Use unique passwords for different accounts (use a password manager)
- Keep software and antivirus updated
- Hover over links before clicking to see actual URL
- Type URLs manually instead of clicking email links for sensitive accounts
- Regularly review account activity for suspicious logins
- Educate yourself about common phishing tactics

**❌ DON'T:**
- Click links or download attachments from unknown senders
- Provide passwords, credit cards, or SSN via email
- Use the same password across multiple accounts
- Trust caller ID or email "From" field alone
- Wire money or buy gift cards based on email requests
- Ignore security warnings from your email provider or browser

## Real-World Examples

### Example 1: PayPal Phishing

**Email Appears As:**
```
From: PayPal Security <service@paypal.com>
Subject: Urgent: Verify your account within 24 hours

Dear Customer,

We've detected unusual activity on your account. To prevent suspension,
please verify your information immediately:

[Verify My Account] ← (Actually links to paypa1-secure.com)

Failure to verify will result in permanent account closure.

PayPal Security Team
```

**Phishing Inspector Detects:**
- 🔴 **Risk Score: 89/100 - PHISHING**
- ❌ SPF authentication failed (not actually from PayPal)
- ❌ URL verification: Malicious link confirmed by Google Safe Browsing and VirusTotal
- ❌ Domain paypa1-secure.com registered 23 days ago
- ❌ Urgency tactic detected (24-hour threat)
- ❌ Generic greeting ("Dear Customer" instead of your name)

**Verdict:** Delete and report. Real PayPal never asks you to verify via email links.

### Example 2: Legitimate Shipping Notification

**Email Appears As:**
```
From: Amazon <ship-confirm@amazon.com>
Subject: Your Amazon.com order has shipped

Hello John Smith,

Your order #123-4567890-1234567 has shipped!

Track your package: [Track Package] ← (Actually links to amazon.com/tracking)

Delivery estimate: November 18, 2025

[View order details]

Thanks for shopping with us!
Amazon.com
```

**Phishing Inspector Detects:**
- 🟢 **Risk Score: 12/100 - LEGITIMATE**
- ✅ SPF, DKIM, DMARC all passed
- ✅ All URLs verified clean by Google Safe Browsing and VirusTotal
- ✅ Links point to legitimate amazon.com domain
- ✅ Personalized greeting with your name
- ✅ Sender IP has excellent reputation
- ✅ No urgency or threat tactics

**Verdict:** Likely legitimate, safe to interact with.

### Example 3: Compromised Friend's Account

**Email Appears As:**
```
From: Sarah Johnson <sarah.j@gmail.com>
Subject: Hey! Check this out

Hi,

I found this article and thought of you!

[Click here to read] ← (Actually links to malicious site)

Let me know what you think!
Sarah
```

**Phishing Inspector Detects:**
- 🟠 **Risk Score: 67/100 - SUSPICIOUS**
- ✅ SPF passed (really from Gmail)
- ❌ URL verification: Link flagged by URLhaus as malware distribution
- ⚠️ Behavioral analysis: Generic message pattern common in compromised accounts
- ⚠️ Short message with suspicious link

**Verdict:** Likely compromised account. Contact Sarah through another method (call/text) to verify before clicking.

## Switching to SOC Analyst Report

For more detailed technical information, click **"View Technical Details"** at the bottom of the Simple Report.

The SOC Analyst Report includes:
- **5-Dimensional Risk Breakdown** with radar chart visualization
- **Complete IOC Extraction**: All URLs, IPs, domains, emails, keywords
- **External Verification Details**: Results from every threat intelligence service
- **AI Model Analysis**: See what both Llama and Gemma detected
- **MITRE ATT&CK Techniques**: Security framework mappings
- **Email Authentication Details**: Full SPF/DKIM/DMARC results
- **IP Reputation**: Abuse scores and blacklist status
- **Attachment Analysis**: File hashes and risk assessment

See the **[SOC Analyst Guide](./soc-analyst-guide.md)** for detailed explanation of advanced features.

## Getting Help

### If You're Unsure
1. Review the Simple Report carefully
2. Check external verification badges (Google, VirusTotal)
3. Look at confidence score (higher = more certain)
4. Switch to SOC Analyst Report for more details
5. When in doubt, verify through official channels

### Common Issues
- **Error messages**: See [Troubleshooting Guide](../troubleshooting/common-issues.md)
- **Body-only mode confusion**: See [Mobile Workflows](../workflows/mobile-devices.md)
- **Email client help**: See [Email Client Workflows](../workflows/email-clients.md)
- **More questions**: Check [FAQ](../troubleshooting/faq-extended.md)

### Additional Resources
- **Main Application**: [phishinginspector.com](https://www.phishinginspector.com)
- **Technical Documentation**: [Technical Architecture](../technical-reference/architecture.md)
- **Report Phishing**: [reportphishing@apwg.org](mailto:reportphishing@apwg.org)
- **FBI Internet Crime Complaint**: [ic3.gov](https://www.ic3.gov)

---

## Quick Checklist

Before clicking any link in an email, ask yourself:

- [ ] Did I request this email or expect it?
- [ ] Does the sender address look correct?
- [ ] Is the greeting personalized with my name?
- [ ] Are there spelling or grammar errors?
- [ ] Is there urgent or threatening language?
- [ ] Does it request sensitive information?
- [ ] Have I analyzed it with Phishing Inspector?
- [ ] Does the verdict and risk score make sense?
- [ ] Have I verified unexpected requests through official channels?

**When in doubt, don't click!** Legitimate companies will understand you verifying their requests through official channels.

---

**Stay safe online!** Use Phishing Inspector as one tool in your security toolkit, combined with healthy skepticism and verification of unexpected requests.
