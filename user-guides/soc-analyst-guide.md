# SOC Analyst Guide

This guide is designed for security professionals, SOC analysts, and IT security teams who need detailed technical analysis of suspicious emails for incident response, threat hunting, and security operations.

## Table of Contents
- [Overview](#overview)
- [SOC Analyst Report Features](#soc-analyst-report-features)
- [5-Dimensional Risk Analysis](#5-dimensional-risk-analysis)
- [IOC Extraction and Categorization](#ioc-extraction-and-categorization)
- [External Verification Deep Dive](#external-verification-deep-dive)
- [AI Model Analysis](#ai-model-analysis)
- [Email Authentication Analysis](#email-authentication-analysis)
- [MITRE ATT&CK Mappings](#mitre-attck-mappings)
- [Confidence Scoring Algorithm](#confidence-scoring-algorithm)
- [Integration with Security Workflows](#integration-with-security-workflows)
- [Advanced Use Cases](#advanced-use-cases)

## Overview

### Target Audience
- SOC Analysts
- Incident Response Teams
- Threat Intelligence Analysts
- Security Engineers
- IT Security Administrators
- Blue Team Members

### What Makes the SOC Report Different

The SOC Analyst Report provides comprehensive technical data suitable for:
- **Incident Response**: Full IOC extraction and threat intelligence correlation
- **Threat Hunting**: MITRE ATT&CK technique identification and behavioral analysis
- **Forensics**: Complete email authentication and routing path analysis
- **Documentation**: Detailed findings with evidence for incident reports
- **SIEM/TIP Integration**: Structured IOC data ready for ingestion


### Analysis Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    EMAIL INPUT (EML/Source)                      │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                ┌───────────▼──────────┐
                │   Content Validator   │
                │  (Completeness Check) │
                └───────────┬──────────┘
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
┌───────▼───────┐  ┌────────▼────────┐  ┌──────▼──────┐
│ Parser/Norm   │  │  Header Analysis│  │ Attachment  │
│ (Structure)   │  │  (SPF/DKIM/etc) │  │  Analysis   │
└───────┬───────┘  └────────┬────────┘  └──────┬──────┘
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
        ┌───────────────────┴───────────────────┐
        │                                       │
┌───────▼────────┐                    ┌────────▼────────┐
│  AI Models     │                    │ IOC Extraction  │
│  • Llama 3.1   │                    │ • URLs          │
│  • Gemma 2     │                    │ • IPs           │
└───────┬────────┘                    │ • Domains       │
        │                             │ • Emails        │
        │                             └────────┬────────┘
        │                                      │
┌───────▼──────────────────────────────────────▼──────┐
│           External Verification Layer                │
│  • Google Safe Browsing  • VirusTotal               │
│  • URLhaus               • URLScan.io               │
│  • AbuseIPDB             • DNSBL                    │
└───────┬──────────────────────────────────────────────┘
        │
┌───────▼────────┐
│ Risk Calculator│
│ (5 Dimensions) │
└───────┬────────┘
        │
┌───────▼────────┐
│ Report Generator│
│ • Simple Report │
│ • SOC Report    │
└────────────────┘
```

## SOC Analyst Report Features

### Accessing the SOC Report

1. Run email analysis normally
2. After receiving results, click **"View Technical Details"** button
3. Switch back to Simple Report anytime with **"View Simplified Report"**

### Report Sections Overview

The SOC Report uses a tabbed interface for organized access to detailed data:

**Main Dashboard:**
- Executive Summary (AI-generated plain-English overview)
- 5-Dimensional Risk Breakdown (with progress bars)
- Risk Gauge Visualization (0-100 score with color coding)
- Radar Chart (multi-dimensional risk visualization)

**Tabs:**
1. **IOCs** - Indicators of Compromise with detailed analysis
2. **External APIs** - Verification results from all threat intelligence services
3. **Models** - AI model analysis and consensus
4. **Headers** - Email authentication and routing
5. **MITRE** - ATT&CK technique mappings
6. **Actions** - Recommendations and detailed findings


## 5-Dimensional Risk Analysis

### Risk Dimensions Explained

#### 1. Content Risk (Weight: 35%)

**What It Measures:**
- AI model categorization (PHISHING, SPAM, LEGITIMATE, COMMERCIAL)
- Linguistic patterns and phishing indicators
- Social engineering tactic detection
- Keyword analysis (urgent language, financial terms, threats)

**Scoring Logic:**
- **90-100**: Both AI models strongly categorize as PHISHING + high social engineering scores
- **70-89**: One or both models categorize as PHISHING with confidence >70%
- **40-69**: Mixed signals or SPAM categorization
- **0-39**: Both models categorize as LEGITIMATE with high confidence

**Influenced By:**
- Llama 3.1 8B categorization (50% weight)
- Gemma 2 2B categorization (50% weight)
- Behavioral analysis modifiers (+/- 15%)
- Content completeness (partial content reduces by 10-20%)

**Example:**
```
Content Risk: 78/100

Contributing Factors:
• Llama 3.1 8B: PHISHING (confidence: 87%)
• Gemma 2 2B: PHISHING (confidence: 82%)
• Social engineering: Urgency + Authority tactics detected
• Keywords: "verify account", "suspend", "immediate action"
```

#### 2. URL Risk (Weight: 30%)

**What It Measures:**
- External threat intelligence verification
- URL structure and pattern analysis
- Domain age and reputation
- Redirection and obfuscation detection

**Scoring Logic:**
- **90-100**: One or more URLs confirmed malicious by Google Safe Browsing, VirusTotal, URLhaus, or URLScan.io
- **70-89**: Suspicious URL patterns + newly registered domains + failed partial verification
- **40-69**: Mixed signals (some suspicious patterns but no external confirmation)
- **0-39**: All URLs verified clean by threat intelligence services OR no URLs present

**External Verification Priority:**
1. **Google Safe Browsing** (highest priority - used by billions)
2. **VirusTotal** (3+ engines flagging = confirmed threat)
3. **URLhaus** (malware distribution database)
4. **URLScan.io** (detailed scanning and historical data)

**Example:**
```
URL Risk: 95/100

2 URLs extracted, 2 verified as MALICIOUS:

1. hxxp://paypa1-verify[.]tk/login
   • Google Safe Browsing: PHISHING (threat type: SOCIAL_ENGINEERING)
   • VirusTotal: 14/91 engines flagged (MALICIOUS)
   • URLhaus: Listed (threat: phishing)
   • Domain age: 12 days (newly registered)

2. hxxp://bit[.]ly/AbC123 → redirects to same malicious domain
   • URLScan.io: Malicious (verdict score: 0/100)
```

#### 3. Header Risk (Weight: 20%)

**What It Measures:**
- Email authentication protocol validation (SPF, DKIM, DMARC)
- IP address reputation
- Email routing path analysis
- Header forgery detection

**Scoring Logic:**
- **90-100**: Multiple authentication failures + IP blacklisted + suspicious routing
- **70-89**: One or more authentication failures + moderate IP abuse score
- **40-69**: Soft-fail authentication or neutral IP reputation
- **0-39**: All authentication passed + clean IP reputation

**Authentication Priorities:**
- **DMARC fail**: Highest concern (domain explicitly rejects)
- **SPF fail**: Strong indicator of spoofing
- **DKIM fail**: Email modified or forged

**Not Available:** Body-only mode (mobile) - Header Risk set to 0 with explanatory note

**Example:**
```
Header Risk: 82/100

Authentication Results:
• SPF: FAIL (IP 185.234.219.71 not authorized by paypal.com)
• DKIM: NONE (no signature present)
• DMARC: FAIL (domain policy: reject)

IP Reputation (185.234.219.71):
• AbuseIPDB: 87% abuse confidence (142 reports)
• DNSBL: Listed on Spamhaus ZEN, SpamCop
• Location: Russia (mismatched with claimed sender: USA)
• ISP: Unknown hosting provider
```

#### 4. Attachment Risk (Weight: 10%)

**What It Measures:**
- File type risk assessment
- Macro and executable detection
- Archive analysis (compressed files)
- Hash generation for threat intelligence lookup

**Scoring Logic:**
- **90-100**: Executables (.exe, .scr, .bat), macro-enabled docs, double extensions
- **70-89**: Archives (.zip, .rar) containing high-risk files
- **40-69**: Office documents or PDFs (moderate risk)
- **0-39**: Images, plain text, or no attachments

**High-Risk File Types:**
- Executables: .exe, .scr, .bat, .cmd, .com, .pif
- Scripts: .js, .vbs, .ps1, .sh
- Macro-enabled: .docm, .xlsm, .pptm
- Archives: .zip, .rar, .7z (especially with executables inside)

**Example:**
```
Attachment Risk: 95/100

1 attachment detected:

invoice_payment.pdf.exe (327 KB)
• Risk Level: CRITICAL
• Actual Type: Windows Executable (PE32)
• Double Extension: Disguised as PDF
• SHA256: a3f5d...9e2c1
• Threat: Likely malware dropper
```

#### 5. Behavioral Risk (Weight: 5%)

**What It Measures:**
- Social engineering tactics
- Psychological manipulation patterns
- Impersonation techniques
- Urgency and threat language

**Scoring Logic:**
- **90-100**: Multiple social engineering tactics + impersonation + severe urgency
- **70-89**: 2-3 tactics detected
- **40-69**: Single tactic or minor urgency
- **0-39**: No manipulation patterns detected

**Detected Tactics:**
- **Urgency**: "within 24 hours", "immediate action required"
- **Authority**: Impersonating executives, government, law enforcement
- **Fear**: Account suspension, legal action, security breach
- **Curiosity**: "You have a package", unexpected prizes
- **Greed**: Lottery winnings, inheritance, refunds
- **Trust Exploitation**: Compromised friend accounts, brand impersonation

**Example:**
```
Behavioral Risk: 75/100

Social Engineering Tactics Detected:
• URGENCY: "Account will be suspended in 24 hours"
• FEAR: "Unusual login activity detected"
• AUTHORITY: Impersonating PayPal security team
• TRUST: Using official PayPal branding and logo

Manipulation Score: High
Impersonation Confidence: 89%
```

### Risk Score Calculation Formula

```
Overall Risk = (Content × 0.35) + (URL × 0.30) + (Header × 0.20) +
               (Attachment × 0.10) + (Behavioral × 0.05)

With adjustments:
• External verification override: If URLs confirmed malicious, Overall Risk minimum 70
• Authentication override: If all auth passed + all URLs clean, Overall Risk maximum 35
• Body-only mode: Header weight redistributed to Content (45%) and URL (35%)
```

### Radar Chart Visualization

The 5-dimensional radar chart provides instant visual pattern recognition:


**Interpretation Patterns:**

**Phishing (High Risk):**
- Large, balanced pentagon (high scores across dimensions)
- Particularly high Content and URL risks

**Spam:**
- High Content and Behavioral, low URL and Header
- Often one-sided toward Content

**Legitimate:**
- Small, tight shape near center
- Balanced low scores across all dimensions

**Suspicious/Mixed Signals:**
- Irregular shape with some high, some low
- Indicates conflicting evidence requiring manual review

## IOC Extraction and Categorization

### URLs Tab

**Data Provided:**
- Complete URL with protocol
- Root domain extraction
- Reputation status (Malicious, Suspicious, Clean, Unknown)
- Reasons for flagging
- External verification results

**Reputation Categories:**

**MALICIOUS:**
- Confirmed by Google Safe Browsing, VirusTotal (3+ engines), URLhaus, or URLScan.io
- Badge: Red "Malicious" with "Externally verified" note

**SUSPICIOUS:**
- Newly registered domain (<180 days)
- Typosquatting patterns (paypa1.com, micros0ft.com)
- Unusual TLDs (.tk, .ml, .ga, .cf, .gq)
- URL shorteners without verification
- Badge: Orange "Suspicious"

**CLEAN:**
- Verified by external services with no threats
- Known legitimate domains
- Badge: Green "Clean" with "Externally verified"

**UNKNOWN:**
- Not checked by external services (API not configured or rate limited)
- No suspicious patterns detected
- Badge: Gray "Unknown"


**Example Table:**
```
┌────────────────────────────────────────────────────────────────────────┐
│ URL                          │ Domain        │ Status     │ Reasons    │
├────────────────────────────────────────────────────────────────────────┤
│ hxxp://paypa1-verify.tk/login │ paypa1-verify │ MALICIOUS  │ Google Safe│
│                               │ .tk           │ (verified) │ Browsing,  │
│                               │               │            │ VirusTotal │
│                               │               │            │ 14 engines │
├────────────────────────────────────────────────────────────────────────┤
│ https://www.paypal.com        │ paypal.com    │ CLEAN      │ Verified   │
│                               │               │ (verified) │ clean by   │
│                               │               │            │ all services│
└────────────────────────────────────────────────────────────────────────┘
```

### Email Addresses Tab

**Data Provided:**
- Complete email address
- Domain extraction
- Role identification (Sender, Reply-To, CC, BCC)
- Relationship to email flow

**Key Indicators:**
- **Mismatched Sender/Reply-To**: Different domains may indicate phishing
- **Free Email Providers**: gmail.com, yahoo.com for business communications (red flag)
- **Lookalike Domains**: paypa1@gmail.com instead of service@paypal.com

**Example:**
```
┌────────────────────────────────────────────────────────────────┐
│ Email                    │ Domain       │ Role              │
├────────────────────────────────────────────────────────────────┤
│ service@paypa1-verify.tk │ paypa1-verify│ Sender            │
│                          │ .tk          │                   │
├────────────────────────────────────────────────────────────────┤
│ collect@phisher.ru       │ phisher.ru   │ Reply-To ⚠️       │
│                          │              │ (MISMATCH)        │
└────────────────────────────────────────────────────────────────┘
```

### Domains Tab

**Data Provided:**
- Domain name
- Reputation (Malicious, Suspicious, Legitimate, Unknown)
- Age in days
- Registration date
- Registrar information
- Newly registered flag (<180 days)

**Domain Age Significance:**
- **0-30 days**: Extremely suspicious (many phishing campaigns)
- **31-90 days**: Suspicious (common phishing age range)
- **91-180 days**: Newly registered (monitored)
- **181+ days**: Established (lower risk, but still verifiable)


**Example:**
```
┌──────────────────────────────────────────────────────────────────────────┐
│ Domain           │ Status      │ Age        │ Registrar              │
├──────────────────────────────────────────────────────────────────────────┤
│ paypa1-verify.tk │ MALICIOUS   │ 12 days    │ Freenom (free TLD)     │
│                  │ NEW DOMAIN  │ (Oct 2025) │                        │
├──────────────────────────────────────────────────────────────────────────┤
│ paypal.com       │ LEGITIMATE  │ 9,487 days │ MarkMonitor Inc.       │
│                  │             │ (1996)     │                        │
└──────────────────────────────────────────────────────────────────────────┘
```

### IP Addresses Tab

**Data Provided:**
- IP address (extracted from email headers)
- Geographic location
- Reputation (AbuseIPDB score, DNSBL status)
- ISP information
- Abuse reports count

**Reputation Thresholds:**
- **75-100% abuse score**: High risk (active malicious actor)
- **50-74%**: Moderate risk (compromised infrastructure)
- **25-49%**: Low risk (some abuse reports)
- **0-24%**: Clean (few or no reports)

**DNSBL (DNS Blacklist) Sources:**
- Spamhaus ZEN (largest, most trusted)
- SpamCop (user-reported spam)
- Barracuda (enterprise email security)
- SORBS (spam and open relay database)

**Example:**
```
┌────────────────────────────────────────────────────────────────────────┐
│ IP              │ Location │ Reputation  │ Details                   │
├────────────────────────────────────────────────────────────────────────┤
│ 185.234.219.71  │ Russia   │ 87% Abuse   │ AbuseIPDB: 142 reports    │
│                 │ Moscow   │ BLACKLISTED │ DNSBL: Spamhaus, SpamCop  │
│                 │          │             │ ISP: Unknown hosting       │
└────────────────────────────────────────────────────────────────────────┘
```

### Suspicious Keywords Tab

**Data Provided:**
- Extracted high-risk keywords and phrases
- Context importance

**Categories:**
- **Financial**: "wire transfer", "account verification", "credit card"
- **Urgency**: "immediate", "within 24 hours", "expires soon"
- **Threats**: "suspended", "locked", "legal action"
- **Authority**: "IRS", "FBI", "CEO", "security team"
- **Action**: "click here", "verify now", "confirm identity"

### Attachments Tab

**Data Provided:**
- Filename
- Declared MIME type
- Actual file type (magic byte analysis)
- File size
- Risk level (Critical, High, Medium, Low)
- SHA-256 hash
- Analysis reasons

**Example:**
```
┌────────────────────────────────────────────────────────────────────────┐
│ Filename              │ Type   │ Size   │ Risk     │ Analysis        │
├────────────────────────────────────────────────────────────────────────┤
│ invoice_Q4.pdf.exe    │ PE32   │ 327 KB │ CRITICAL │ • Executable    │
│                       │        │        │          │ • Double ext.   │
│                       │        │        │          │ • Disguised     │
│ SHA256: a3f5d...9e2c1 │        │        │          │                 │
└────────────────────────────────────────────────────────────────────────┘
```

## External Verification Deep Dive

### External APIs Tab

This tab shows detailed results from every threat intelligence service queried.


### Google Safe Browsing

**What It Checks:**
- Phishing URLs
- Malware distribution sites
- Unwanted software
- Social engineering pages

**Result Statuses:**
- **MALICIOUS**: Threat detected (includes threat type: MALWARE, SOCIAL_ENGINEERING, UNWANTED_SOFTWARE)
- **CLEAN**: No threats found
- **NOT_FOUND**: URL not in database (not necessarily safe)
- **Failed**: API error or not configured

**Confidence Level:** Highest (used by Chrome, Firefox, Safari - billions of users)

**Example:**
```
Google Safe Browsing: MALICIOUS
• Threat Type: SOCIAL_ENGINEERING
• Platform: ANY_PLATFORM
• Threat Entry Type: URL
• Added to list: 2025-11-14 08:23:41 UTC
```

### VirusTotal

**What It Checks:**
- 70+ antivirus engines
- URL reputation services
- Domain and IP reputation
- Historical scan data

**Result Statuses:**
- **MALICIOUS**: 3 or more engines flagged (threshold configurable)
- **CLEAN**: Scanned by multiple engines, no threats
- **NOT_FOUND**: URL not previously scanned
- **Failed**: API error, rate limit, or not configured

**Confidence Level:** Very High (multi-engine consensus)

**Details Provided:**
- Number of engines that flagged
- Total engines that scanned
- Categories (phishing, malware, spam)
- Last analysis date

**Example:**
```
VirusTotal: MALICIOUS
• Engines detected: 14/91
• Categories: phishing, malicious
• Vendors flagging:
  - Fortinet: Phishing
  - Kaspersky: HEUR:Trojan.Script.Generic
  - ESET: JS/Phishing.Agent
  - BitDefender: Trojan.GenericKD
  [... 10 more]
• Last analysis: 2025-11-16 12:45:32 UTC
• Permalink: virustotal.com/gui/url/[hash]
```

### URLhaus

**What It Checks:**
- Known malware distribution URLs
- Payload delivery sites
- Exploit kits
- Command & control servers

**Result Statuses:**
- **MALICIOUS**: URL in URLhaus database (includes threat type and tags)
- **CLEAN**: Not in malware database
- **NOT_FOUND**: URL not listed (doesn't mean safe, just not in this specific database)
- **Failed**: API error or timeout

**Confidence Level:** High (specialized malware focus)

**Details Provided:**
- Threat classification
- Malware family (if known)
- First seen date
- Reporter information

**Example:**
```
URLhaus: MALICIOUS
• Threat: malware_download
• Tags: emotet, trojan
• Malware Family: Emotet
• First Seen: 2025-11-15 09:12:05 UTC
• Status: Active (online)
• Reporter: abuse_ch
```

### URLScan.io

**What It Checks:**
- Live webpage scanning
- Screenshot analysis
- Network requests
- JavaScript execution
- Historical verdicts

**Result Statuses:**
- **MALICIOUS**: Verdict score 0-40 (suspicious/malicious)
- **SUSPICIOUS**: Verdict score 41-60
- **CLEAN**: Verdict score 61-100
- **NOT_FOUND**: Not previously scanned
- **Failed**: Scan timeout or error

**Confidence Level:** High (detailed live analysis)

**Details Provided:**
- Verdict score (0-100, lower = more malicious)
- Categories and tags
- Technologies detected
- Screenshot availability
- Associated domains and IPs

**Example:**
```
URLScan.io: MALICIOUS
• Verdict Score: 15/100
• Result: Malicious
• Categories: phishing, credential-theft
• Technologies: PHP, Bootstrap
• Brands detected: PayPal (impersonation)
• Screenshot: Available
• Scan UUID: [uuid]
• Permalink: urlscan.io/result/[uuid]
```

### AbuseIPDB

**What It Checks:**
- IP address abuse reports from network administrators worldwide
- Attack types (brute force, spam, DDoS, etc.)
- Historical abuse pattern
- ISP and geolocation

**Result Statuses:**
- **MALICIOUS**: Abuse score 50%+ (or any reports for high-sensitivity)
- **CLEAN**: 0% abuse score or very low (<25%)
- **SUSPICIOUS**: 25-49% abuse score
- **Failed**: API error, rate limit, or not configured

**Confidence Level:** High (community-driven, enterprise-trusted)

**Details Provided:**
- Abuse confidence score (0-100%)
- Total number of reports
- Distinct reporters
- Last reported date
- ISP information
- Country code
- Usage type (ISP, hosting, etc.)

**Example:**
```
AbuseIPDB: MALICIOUS
• Abuse Confidence Score: 87%
• Total Reports: 142
• Distinct Reporters: 67
• Last Reported: 2025-11-16 (2 days ago)
• Country: Russia (RU)
• ISP: Unknown Hosting Provider
• Usage Type: Data Center/Web Hosting/Transit
• Categories: Brute-Force (94), SSH (18), Phishing (12)
```

### DNSBL (DNS Blacklists)

**What It Checks:**
- Multiple DNS-based blacklist services
- Spam sources
- Known malicious IPs
- Open relays and proxies

**Checked Services:**
- **Spamhaus ZEN** (most comprehensive)
- **SpamCop** (user-reported spam)
- **Barracuda** (enterprise email security)
- **SORBS** (various abuse types)

**Result Statuses:**
- **BLACKLISTED**: Listed on one or more DNSBLs (shows which ones)
- **CLEAN**: Not listed on any checked DNSBLs
- **Failed**: DNS resolution error

**Example:**
```
DNSBL: BLACKLISTED
• Listed on: 2/4 blacklists
  ✓ Spamhaus ZEN (SBL/CSS)
  ✓ SpamCop
  ✗ Barracuda
  ✗ SORBS
• Listing reason: Known spam source
• Delisting info: Visit spamhaus.org/lookup
```

## AI Model Analysis

### Models Tab Overview

View detailed analysis from both AI models used for content categorization.


### Model Registry

**Primary Phishing Detection Models:**

**1. Llama 3.1 8B Instruct (meta-llama/Llama-3.1-8B-Instruct)**
- **Purpose**: Primary phishing detection and content analysis
- **Context Window**: 128K tokens (excellent for long emails)
- **Strengths**: Deep understanding of social engineering, nuanced language analysis
- **Processing Time**: 3-6 seconds typical
- **HuggingFace**: [View Model Card](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct)

**2. Gemma 2 2B IT (google/gemma-2-2b-it)**
- **Purpose**: Fast categorization and consensus validation
- **Context Window**: 8K tokens
- **Strengths**: Speed, efficiency, general phishing pattern recognition
- **Processing Time**: 1-2 seconds typical
- **HuggingFace**: [View Model Card](https://huggingface.co/google/gemma-2-2b-it)

### Model Output Structure

Each model provides:

**Categorization:**
- PHISHING
- SPAM
- LEGITIMATE
- COMMERCIAL

**Confidence Score (0-100%):**
- 90-100%: Very high confidence
- 75-89%: High confidence
- 50-74%: Medium confidence
- <50%: Low confidence (model unsure)

**Human-Readable Label:**
- Translated from technical labels for clarity

**Short Description:**
- One-sentence summary of finding

**Full Explanation:**
- Detailed reasoning for categorization

**Impact Assessment:**
- Potential consequences if email is malicious

**Severity:**
- danger (high risk)
- warning (medium risk)
- safe (low risk)
- info (informational)

**Processing Time:**
- Milliseconds taken for analysis

### Example Model Card

```
┌─────────────────────────────────────────────────────────────────┐
│ Llama 3.1 8B Instruct - Phishing Detection                     │
│ Model Purpose: Advanced phishing and social engineering detect │
├─────────────────────────────────────────────────────────────────┤
│ Verdict: PHISHING                                              │
│ Confidence: 87%                                                 │
│ Severity: DANGER                                                │
├─────────────────────────────────────────────────────────────────┤
│ Short Description:                                              │
│ High-confidence phishing attempt impersonating PayPal with     │
│ multiple red flags including urgent language and malicious URL │
├─────────────────────────────────────────────────────────────────┤
│ Full Explanation:                                               │
│ This email exhibits classic phishing characteristics:          │
│ 1. Creates false urgency with 24-hour deadline                 │
│ 2. Threatens account suspension                                │
│ 3. Requests credential verification via external link          │
│ 4. Uses generic greeting despite claiming account-specific     │
│ 5. Contains typosquatted domain (paypa1 vs paypal)            │
│ 6. Sender authentication failed                                │
│                                                                 │
│ The combination of social engineering tactics, authentication  │
│ failures, and malicious URL strongly indicates phishing.       │
├─────────────────────────────────────────────────────────────────┤
│ Impact Assessment:                                              │
│ If victim clicks link and enters credentials, attacker gains   │
│ full access to PayPal account enabling unauthorized            │
│ transactions, identity theft, and financial fraud.             │
├─────────────────────────────────────────────────────────────────┤
│ Processing Time: 4,287 ms                                       │
└─────────────────────────────────────────────────────────────────┘
```

### Model Consensus Algorithm

**Agreement Levels:**

**100% Consensus (Both Agree):**
- Both models produce same categorization
- Highest confidence in verdict
- Minimal adjustment to confidence score

**67% Consensus (Majority):**
- Models disagree but one has significantly higher confidence
- Majority opinion taken with moderate confidence
- Confidence score adjusted down by 5-8%

**50% Consensus (Tie):**
- Models produce different categorizations with similar confidence
- External verification heavily weighted
- Confidence score adjusted down by 8-12%
- Flags for manual review

**33% Consensus (Strong Disagreement):**
- Models strongly disagree
- External verification becomes primary factor
- Confidence score significantly reduced (15-20%)
- Requires SOC analyst review

**Example Consensus Scenarios:**

```
Scenario 1: Perfect Agreement
┌──────────────┬───────────┬────────────┬──────────────────┐
│ Model        │ Category  │ Confidence │ Final Verdict    │
├──────────────┼───────────┼────────────┼──────────────────┤
│ Llama 3.1    │ PHISHING  │ 87%        │ PHISHING         │
│ Gemma 2      │ PHISHING  │ 82%        │ Confidence: 92%  │
│              │           │            │ (boosted +10%)   │
└──────────────┴───────────┴────────────┴──────────────────┘

Scenario 2: Disagreement Resolved by External Verification
┌──────────────┬───────────┬────────────┬──────────────────┐
│ Model        │ Category  │ Confidence │ Final Verdict    │
├──────────────┼───────────┼────────────┼──────────────────┤
│ Llama 3.1    │ LEGITIMATE│ 72%        │ PHISHING         │
│ Gemma 2      │ SUSPICIOUS│ 65%        │ Confidence: 88%  │
│              │           │            │                  │
│ External:    │ Google Safe Browsing:  │ External verification│
│              │ MALICIOUS              │ overrides models │
└──────────────┴───────────┴────────────┴──────────────────┘
```

## Email Authentication Analysis

### Headers Tab

Comprehensive email authentication and routing analysis.


### SPF (Sender Policy Framework)

**What It Validates:**
- Whether sending IP is authorized by domain owner
- Checks DNS TXT records for authorized mail servers

**Results:**
- **pass**: Sender IP authorized ✅
- **fail**: Sender IP NOT authorized (strong spoofing indicator) ❌
- **softfail**: Likely unauthorized (~softfail) ⚠️
- **neutral**: No policy or neutral policy ⚠️
- **none**: No SPF record exists ⚠️
- **temperror**: Temporary DNS error ⚠️
- **permerror**: Permanent error in SPF record ⚠️

**Interpretation:**
```
SPF: FAIL
• Result: IP 185.234.219.71 not authorized by paypal.com
• SPF Record: v=spf1 ip4:66.211.160.0/19 ip4:66.211.176.0/20 ~all
• Risk: HIGH - Sender impersonating PayPal domain
```

### DKIM (DomainKeys Identified Mail)

**What It Validates:**
- Email has not been modified in transit
- Cryptographic signature verification
- Confirms email originated from claimed domain

**Results:**
- **pass**: Signature valid, email unmodified ✅
- **fail**: Signature invalid or verification failed ❌
- **none**: No DKIM signature present ⚠️
- **neutral**: Signature present but not verified ⚠️
- **temperror**: Temporary failure ⚠️
- **permerror**: Permanent error ⚠️

**Interpretation:**
```
DKIM: NONE
• No DKIM signature found
• Expected for legitimate PayPal emails
• Risk: MODERATE - Cannot verify email integrity
```

### DMARC (Domain-based Message Authentication)

**What It Validates:**
- Overall authentication policy enforcement
- Combines SPF and DKIM results
- Domain owner's instruction for handling failures

**Results:**
- **pass**: Authenticated (SPF or DKIM passed and aligned) ✅
- **fail**: Authentication failed per domain policy ❌
- **none**: No DMARC policy exists ⚠️

**DMARC Policies:**
- **none**: No action (monitoring only)
- **quarantine**: Move to spam folder
- **reject**: Bounce email (strict)

**Interpretation:**
```
DMARC: FAIL
• Policy: reject (p=reject)
• Alignment: FAIL (SPF failed, no DKIM)
• Domain owner (paypal.com) explicitly rejects this email
• Risk: CRITICAL - Confirmed unauthorized sender
```

### Authentication Scoring Impact

```
All Pass (SPF + DKIM + DMARC):
→ Header Risk: 0-10 (minimal)
→ Overall Risk: Reduced by 15-25 points
→ Confidence: Increased by 10-15%

SPF or DKIM Fail:
→ Header Risk: 60-75 (high)
→ Overall Risk: Increased by 20-30 points
→ Confidence: Standard

Multiple Failures + DMARC Reject:
→ Header Risk: 85-100 (critical)
→ Overall Risk: Increased by 30-40 points
→ Verdict: Likely PHISHING regardless of content
```

### Email Routing Path

**Received Headers Analysis:**
- Traces email journey through mail servers
- Shows chronological path (oldest to newest)
- Identifies origin server and all hops

**Example:**
```
Email Path (4 hops):
1. From: unknown [185.234.219.71] (Russia)
   To: mail.relay.com
   Time: 2025-11-16 10:23:41 UTC

2. From: mail.relay.com [54.123.45.67] (USA)
   To: mx.google.com
   Time: 2025-11-16 10:23:43 UTC

3. From: mx.google.com [172.253.115.26] (USA)
   To: gmail-smtp-in.google.com
   Time: 2025-11-16 10:23:44 UTC

4. Delivered to: victim@gmail.com
   Time: 2025-11-16 10:23:45 UTC

⚠️ Origin mismatch: Email claims to be from PayPal (USA) but
   originated from unknown server in Russia
```

### Suspicious Header Patterns

**Detected Anomalies:**
- Mismatched Message-ID domains
- Forged Received headers
- Inconsistent time zones
- Unusual header sequence
- Modified or stripped headers

**Example:**
```
Suspicious Header Patterns Detected:

1. Return-Path mismatch
   • From: service@paypal.com
   • Return-Path: <collect@phisher.ru>
   → Reply will go to different address

2. Message-ID anomaly
   • Claims origin: paypal.com
   • Message-ID: <random@phisher.tk>
   → Forged sender identification

3. X-Mailer suspicion
   • X-Mailer: Microsoft Outlook Express 6.00.2600.0000
   → Outdated client commonly used by spammers
```

## MITRE ATT&CK Mappings

### MITRE Tab Overview

Maps detected techniques to the MITRE ATT&CK framework for standardized threat classification.


### Common Techniques Detected

#### T1566.002: Phishing - Spearphishing Link

**Description:**
Adversaries send spearphishing messages with malicious links to gain access to victim systems or steal credentials.

**Detection Criteria:**
- Email contains URLs to phishing sites
- Social engineering tactics present
- Credential harvesting page suspected

**Example Mapping:**
```
T1566.002: Phishing: Spearphishing Link
Tactic: Initial Access
Description: Email contains link to credential phishing page impersonating
PayPal. URL verified as malicious by Google Safe Browsing and VirusTotal.

Evidence:
• Malicious URL: hxxp://paypa1-verify[.]tk/login
• Typosquatted domain (paypa1 vs paypal)
• Requests account credentials
• Creates urgency for immediate action
```

#### T1566.001: Phishing - Spearphishing Attachment

**Description:**
Adversaries send spearphishing messages with malicious attachments to gain access or execute code.

**Detection Criteria:**
- High-risk attachment present (executable, macro-enabled document)
- Social engineering to open attachment
- File type mismatch (double extension)

**Example Mapping:**
```
T1566.001: Phishing: Spearphishing Attachment
Tactic: Initial Access
Description: Email contains executable file disguised as PDF invoice.

Evidence:
• Attachment: invoice_Q4.pdf.exe (PE32 executable)
• Double extension obfuscation
• Social engineering: "Open immediately for payment processing"
• Unsigned executable
```

#### T1598.003: Phishing for Information - Spearphishing Service

**Description:**
Adversaries send targeted messages via electronic services to gather information.

**Detection Criteria:**
- Requests for personal/financial information
- No immediate malware delivery
- Information gathering focus

**Example Mapping:**
```
T1598.003: Phishing for Information: Spearphishing Service
Tactic: Reconnaissance
Description: Email requests account verification and personal information update.

Evidence:
• Requests: Account number, SSN, DOB, passwords
• No malicious files
• Information collection focus
• Impersonates trusted service
```

#### T1534: Internal Spearphishing

**Description:**
Adversaries use compromised accounts to send phishing messages to targets within the organization.

**Detection Criteria:**
- Email from known/legitimate account
- Unusual content for sender
- Authentication passed but suspicious content
- Often detected via behavioral analysis

**Example Mapping:**
```
T1534: Internal Spearphishing
Tactic: Lateral Movement
Description: Email from compromised colleague account (sarah.j@company.com)
requesting access to sensitive resources.

Evidence:
• SPF/DKIM passed (legitimate account)
• Unusual request pattern for sender
• Generic message inconsistent with sender's style
• Behavioral analysis: High suspicion score
```

### Using MITRE Mappings

**For Incident Response:**
1. Identify attacker tactics and techniques
2. Reference MITRE for detailed mitigation strategies
3. Check if technique matches known threat actors/campaigns
4. Update detection rules and hunting queries

**For Threat Intelligence:**
1. Correlate techniques across multiple incidents
2. Identify campaign patterns
3. Share IOCs and TTPs with community
4. Update threat models

**For Documentation:**
1. Standardized technique IDs for reporting
2. Common language across security teams
3. Executive communication with framework backing
4. Compliance and audit trails

## Confidence Scoring Algorithm

### Base Confidence

**Starting Point:**
- Primary AI model (Llama 3.1) confidence score (0-100%)

### Adjustments

**Content Completeness:**
- **Body-only mode**: -15%
- **Missing headers (partial)**: -12%
- **Partial content**: -8%

**External Verification:**
- **All URLs clean + auth passed**: -15%
- **Risk override applied**: -20%
- **Google/VirusTotal confirmed threat**: +10%

**Model Consensus:**
- **Perfect consensus (100%)**: +10%
- **Strong consensus (67%+)**: +5%
- **Low consensus (<34%)**: -8%

**Mixed Signals:**
- **Multiple contradictions**: -10%
- **High content risk + clean URLs + passed auth**: -15%

**Final Formula:**
```
Confidence = BASE_CONFIDENCE + ΣADJUSTMENTS

Clamped to range: [45%, 95%]
```

**Example Calculation:**
```
Base (Llama 3.1): 87%
+ Perfect consensus: +10%
- Body-only mode: -15%
+ External verification (Google confirmed): +10%
─────────────────
Final Confidence: 92%
```

### Confidence Interpretation

**90-95% (Very High):**
- Multiple layers confirm verdict
- External verification matches AI analysis
- Complete data available
- Action: High confidence for automated response

**75-89% (High):**
- Strong evidence across most layers
- Minor data limitations or single contradiction
- Action: Suitable for most decisions

**60-74% (Medium):**
- Mixed signals or moderate data limitations
- Some layers disagree
- Action: Manual review for critical decisions

**45-59% (Low):**
- Significant contradictions or severe data limitations
- Low model consensus
- Action: Requires analyst judgment

## Integration with Security Workflows

### SIEM Integration

**Structured IOC Export (Conceptual):**
```json
{
  "verdict": "PHISHING",
  "risk_score": 89,
  "confidence": 92,
  "timestamp": "2025-11-16T10:23:45Z",
  "iocs": {
    "urls": [
      {
        "url": "http://paypa1-verify.tk/login",
        "reputation": "MALICIOUS",
        "verified_by": ["Google Safe Browsing", "VirusTotal"]
      }
    ],
    "ips": [
      {
        "ip": "185.234.219.71",
        "abuse_score": 87,
        "blacklisted": ["Spamhaus", "SpamCop"]
      }
    ],
    "domains": [
      {
        "domain": "paypa1-verify.tk",
        "age_days": 12,
        "reputation": "MALICIOUS"
      }
    ]
  },
  "mitre_techniques": ["T1566.002"],
  "authentication": {
    "spf": "fail",
    "dkim": "none",
    "dmarc": "fail"
  }
}
```

### Threat Intelligence Platform (TIP)

**Use Cases:**
1. **IOC Enrichment**: Add Phishing Inspector analysis to existing IOC records
2. **Correlation**: Link related campaigns via shared IOCs
3. **Scoring**: Use risk scores and confidence for prioritization
4. **Automation**: Feed verdicts into automated response workflows

### Email Gateway Integration

**Post-Delivery Analysis:**
1. User forwards suspicious email to analysis address
2. Automated parsing and submission to Phishing Inspector
3. Results sent to SOC queue for triage
4. High-risk emails trigger automatic user notification

### Ticketing System Integration

**Incident Creation:**
```
Ticket: Phishing Email Detected
Priority: HIGH
Category: Phishing / Social Engineering

Summary:
Email to user@company.com analyzed as PHISHING (risk: 89/100, confidence: 92%)

IOCs:
- URL: hxxp://paypa1-verify[.]tk/login (MALICIOUS - Google, VirusTotal)
- IP: 185.234.219.71 (87% abuse, Russia)
- Domain: paypa1-verify.tk (12 days old)

MITRE Techniques: T1566.002 (Phishing: Spearphishing Link)

Recommendations:
1. IMMEDIATE: Block URL and domain on email gateway
2. IMMEDIATE: Block IP 185.234.219.71 on firewall
3. HIGH: Search email logs for other deliveries
4. HIGH: Notify affected users
5. MEDIUM: Update phishing awareness training with example

Attachments:
- Full analysis report (PDF)
- Original email (EML)
```

## Advanced Use Cases

### Campaign Analysis

**Identifying Coordinated Attacks:**

1. **Analyze multiple suspicious emails** over time period
2. **Compare IOCs** across reports:
   - Shared URLs, domains, IPs
   - Similar social engineering tactics
   - Common sender patterns
   - Attachment file hashes
3. **Correlation indicators**:
   - Same newly registered domain across emails
   - IP ranges from same ASN
   - Similar AI model explanations
   - Identical MITRE technique combinations

**Example Campaign Detection:**
```
Campaign: "PayPal Verification" Phishing (Nov 2025)

Shared Characteristics (5 emails analyzed):
• Domain pattern: paypa1-*.tk (various subdomains)
• All domains registered: Nov 1-12, 2025
• Same registrar: Freenom
• Originating IPs: 185.234.219.0/24 (Russia)
• Identical social engineering: 24-hour urgency + account suspension
• MITRE: T1566.002 consistent across all

Verdict: Coordinated phishing campaign
Action: Block entire IP range and domain pattern
```

### Threat Hunting

**Proactive Email Security:**

1. **Baseline Analysis**: Analyze legitimate emails from key services (banking, corporate, etc.)
2. **Pattern Learning**: Document normal characteristics:
   - Expected sender IPs
   - Typical authentication results
   - Common language patterns
   - Standard URLs and domains
3. **Anomaly Detection**: Flag emails that deviate:
   - Known sender but different IP range
   - Passed authentication but suspicious content
   - Unusual urgency for typically routine communications

### Training and Awareness

**Using Reports for Education:**

1. **Phishing Simulations**:
   - Run emails through analysis BEFORE sending to users
   - Share reports showing detection indicators
   - Educate on warning signs identified by system

2. **Case Studies**:
   - Export SOC reports as PDF/documentation
   - Annotate real phishing examples
   - Create "phishing vs legitimate" comparison guides
   - Include in security awareness training

3. **Executive Briefings**:
   - Use risk scores and radar charts for visualization
   - Show external verification as "trusted sources agree"
   - Highlight cost of potential breach (Impact Assessments from AI models)

### Forensics and Incident Response

**Post-Incident Analysis:**

1. **Timeline Reconstruction**:
   - Email received timestamp
   - Analysis timestamp
   - IOC first-seen dates (domain age, URLhaus entry, etc.)
   - User interaction events

2. **Scope Assessment**:
   - Search email logs for same IOCs
   - Identify all affected users
   - Determine if credentials were entered
   - Check for similar patterns in other emails

3. **Evidence Collection**:
   - Complete SOC report with all tabs
   - IOC list for SIEM queries
   - Authentication details showing forgery
   - External verification screenshots
   - MITRE technique mappings for reporting

### Red Team / Purple Team

**Testing Email Security:**

1. **Red Team**:
   - Craft phishing emails for testing
   - Analyze with Phishing Inspector to see detectability
   - Adjust tactics to evade specific detection layers
   - Measure organization's response to various risk levels

2. **Purple Team**:
   - Blue team analyzes red team's phishing attempts
   - Compare AI detection vs analyst detection
   - Identify detection gaps
   - Improve both automated and human analysis

### Compliance and Audit

**Documentation Requirements:**

- **PCI DSS 12.6**: Security awareness training - use reports as training material
- **NIST CSF**: Detect function - demonstrate email threat detection capability
- **ISO 27001**: Incident response evidence and documentation
- **SOC 2**: Monitoring and logging of security events

**Audit-Ready Reports:**
- Timestamped analysis
- Multiple independent verification sources (defense in depth)
- Clear verdict with evidence trail
- Standard framework mapping (MITRE)
- Confidence scoring for decision transparency

---

## SOC Analyst Checklist

When reviewing Phishing Inspector SOC reports:

### Initial Assessment
- [ ] Review overall verdict and risk score
- [ ] Check confidence level (>75% preferred for automated actions)
- [ ] Note if body-only mode (limited analysis)
- [ ] Read executive summary for quick context

### Risk Breakdown Analysis
- [ ] Identify highest risk dimensions
- [ ] Check if risk pattern matches verdict (balanced = phishing, uneven = review)
- [ ] Note any contradictions (high content, low URL, etc.)

### IOC Verification
- [ ] Review all extracted URLs - any externally verified as malicious?
- [ ] Check domain ages - newly registered (<180 days)?
- [ ] Examine IP reputation - abuse score >50%?
- [ ] Look for email address mismatches (From vs Reply-To)
- [ ] Review attachments - high-risk file types?

### External Intelligence
- [ ] Confirm Google Safe Browsing results (highest priority)
- [ ] Check VirusTotal consensus (3+ engines significant)
- [ ] Note URLhaus listings (specialized malware focus)
- [ ] Review URLScan.io verdict and score
- [ ] Verify AbuseIPDB abuse confidence
- [ ] Check DNSBL status (Spamhaus most critical)

### Authentication Analysis
- [ ] Check SPF result - fail is strong phishing indicator
- [ ] Review DKIM - fail or none concerning for established senders
- [ ] Verify DMARC - fail with reject policy is critical
- [ ] Examine email routing path - origin matches claimed sender?
- [ ] Note suspicious header patterns

### AI Model Review
- [ ] Check both model categorizations
- [ ] Review confidence scores
- [ ] Read full explanations for reasoning
- [ ] Note any consensus issues
- [ ] Verify impact assessments align with verdict

### MITRE and Context
- [ ] Review mapped techniques
- [ ] Correlate with known campaigns if applicable
- [ ] Check for internal spearphishing indicators
- [ ] Note any advanced techniques

### Decision Making
- [ ] Does verdict align with all evidence?
- [ ] Are there any conflicting indicators requiring manual review?
- [ ] Is confidence high enough for automated action?
- [ ] Should this be escalated or investigated further?
- [ ] Are there related emails to search for (campaign indicators)?

### Action Items
- [ ] Block malicious IOCs (URLs, IPs, domains)
- [ ] Notify affected users if needed
- [ ] Search email logs for similar emails
- [ ] Update detection rules
- [ ] Document in ticketing system
- [ ] Add IOCs to threat intelligence platform
- [ ] Update user training if new technique observed

---

## Best Practices for SOC Teams

### Standard Operating Procedure

1. **Triage (1-2 minutes)**:
   - Quick review of verdict, risk, confidence
   - Check for externally verified threats
   - Determine priority (PHISHING high, LEGITIMATE low)

2. **Analysis (3-5 minutes for high priority)**:
   - Review all IOC tabs
   - Verify external intelligence results
   - Check authentication details
   - Review AI model reasoning

3. **Action (varies)**:
   - Block IOCs on email gateway/firewall
   - Search for related emails
   - Notify users
   - Create incident ticket
   - Update threat intelligence

### Integration Tips

- **Email Submission**: Set up dedicated email address for user reports
- **Automation**: API integration for bulk analysis (if implementing custom solution)
- **Alerting**: High-risk emails (90+) trigger immediate SOC notification
- **Metrics**: Track analysis volume, verdict distribution, false positive rate

### False Positive Handling

**When Legitimate Email Marked PHISHING:**

1. **Review confidence score**: Low confidence (<70%) suggests uncertainty
2. **Check specific findings**: Which layer caused high risk?
3. **Context matters**:
   - Newly registered domain might be legitimate startup
   - Failed SPF could be misconfigured, not malicious
   - Aggressive language might be legitimate marketing
4. **External verification trumps AI**: If all URLs clean + auth passed, likely FP
5. **Feedback loop**: Document patterns for future calibration

### False Negative Handling

**When Phishing Email Marked LEGITIMATE:**

**Indicators:**
1. User reports after clicking suspicious link
2. Known campaign not detected
3. Behavioral anomalies despite low score

**Response:**
1. Review full SOC report for missed indicators
2. Check if body-only mode limited analysis
3. Verify external APIs were active
4. Submit feedback/sample for model improvement
5. Implement compensating controls

---

## Additional Resources

### Technical Documentation
- [Technical Architecture](../technical-reference/architecture.md) - System design details
- [Risk Scoring Methodology](../technical-reference/risk-scoring.md) - Algorithm deep dive
- [External Services](../technical-reference/external-services.md) - API integration details

### Workflows
- [SOC Team Workflows](../workflows/soc-team-workflows.md) - Team collaboration patterns
- [Email Client Workflows](../workflows/email-clients.md) - Extracting email source

### Reference
- [Glossary](../technical-reference/glossary.md) - Security terminology
- [MITRE ATT&CK](https://attack.mitre.org) - Official framework documentation

### External Services
- [Google Safe Browsing API](https://developers.google.com/safe-browsing)
- [VirusTotal](https://www.virustotal.com/gui/home/upload)
- [URLhaus](https://urlhaus.abuse.ch)
- [URLScan.io](https://urlscan.io)
- [AbuseIPDB](https://www.abuseipdb.com)
- [Spamhaus](https://www.spamhaus.org)

---

**Questions or need clarification?** Review the [FAQ](../troubleshooting/faq-extended.md) or [Common Issues](../troubleshooting/common-issues.md) guide.

For normal user documentation, see the **[Normal User Guide](./normal-user-guide.md)**.
