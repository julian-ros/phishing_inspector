# Common Issues & Solutions

Comprehensive troubleshooting guide for Phishing Inspector. Find solutions to errors, warnings, and unexpected behaviors.

## Table of Contents
- [Analysis Errors](#analysis-errors)
- [Warnings and Notices](#warnings-and-notices)
- [Performance Issues](#performance-issues)
- [Unexpected Results](#unexpected-results)
- [Mobile-Specific Issues](#mobile-specific-issues)
- [External Service Issues](#external-service-issues)

---

## Analysis Errors

### Error: "Insufficient content for analysis"

**Error Message:**
```
❌ Error: Insufficient content for analysis
The provided content is too short or doesn't appear to be email-related.
Minimum 50 characters of meaningful content required.
```

**Common Causes:**
1. Copied very short text (less than 50 characters)
2. Copied only subject line or sender
3. Copied placeholder text or instructions
4. Pasted non-email content

**Solutions:**

**For Desktop Users:**
1. Go back to email client
2. Use "Show original" (Gmail) or "View Source" (Outlook)
3. Copy the **complete email source** including all headers and body
4. Verify you copied everything (should be hundreds to thousands of lines)
5. Paste into Phishing Inspector

**For Mobile Users:**
1. Make sure you selected **all** email text
2. Include sender, subject, body, and links
3. Minimum 100+ characters for meaningful analysis
4. If email is very short, consider forwarding to desktop first

**What sufficient content looks like:**
```
From: service@example.com
Subject: Account Verification Required

Dear Customer,

We've detected unusual activity on your account.
Please verify your information by clicking below:

[Verify My Account]

Failure to verify within 24 hours will result in suspension.

Thank you,
Security Team
```

---

### Error: "Invalid email format"

**Error Message:**
```
❌ Error: Invalid email format
Unable to parse email structure. Please provide complete email source.
```

**Common Causes:**
1. Corrupted email source
2. Heavily edited or modified content
3. Screenshot text instead of actual source
4. HTML rendered as plain text incorrectly

**Solutions:**
1. **Don't edit the source**: Copy email exactly as shown in "Show original"
2. **Don't use screenshots**: Must be actual text, not images
3. **Verify complete copy**: Email source should include headers like `Received:`, `From:`, `To:`
4. **Try EML export**: Save email as .eml file and upload instead

---

### Error: "Analysis failed - Please try again"

**Error Message:**
```
❌ Error: Analysis failed
An unexpected error occurred during analysis. Please try again.
```

**Common Causes:**
1. Temporary server issue
2. Extremely large email (>10MB)
3. Corrupted attachment data
4. Network timeout

**Solutions:**
1. **Wait 30 seconds** and click "Analyze" again
2. **Refresh the page** and paste content again
3. **Check internet connection** - ensure stable connection
4. **Try shorter email**: If email is very large, test with smaller sample first
5. **Remove attachments**: If possible, analyze without large attachments
6. **Try different browser**: Switch to Chrome or Firefox if using less common browser

**If problem persists:**
- Email may have unusual formatting that causes processing issues
- Try analyzing a different email to verify system is working
- Report issue with email characteristics (length, number of attachments, etc.)

---

## Warnings and Notices

### Warning: "Mobile/Body-Only Analysis Mode"

**Warning Message:**
```
📱 Mobile/Body-Only Analysis Mode

Analysis performed on email body content without headers (typically from mobile devices).

Available checks: AI content analysis (2 models), URL verification (Google Safe Browsing,
VirusTotal, URLhaus, URLScan.io), Domain age, Behavioral patterns.

Unavailable checks: Email authentication (SPF, DKIM, DMARC), IP reputation, Email routing.

Confidence reduced by 15% due to missing header data.
```

**What It Means:**
- System detected you provided email body WITHOUT headers
- This is **normal for mobile** device usage
- Analysis still valuable but with limitations

**Is This a Problem?**
**No** - This is expected behavior when:
- Analyzing from smartphone/tablet
- Email client doesn't allow header access
- You copied body text instead of using "Show original"

**Can Still Detect:**
- ✅ Phishing content patterns (AI analysis)
- ✅ Malicious URLs (all threat intelligence services)
- ✅ Newly registered domains
- ✅ Social engineering tactics

**Cannot Detect:**
- ❌ Sender authentication failures (SPF, DKIM, DMARC)
- ❌ Sending IP reputation
- ❌ Email routing path anomalies

**Solutions:**

**If on Mobile:**
- This is expected - continue with analysis
- Results are still valuable for most phishing detection
- For highest confidence, forward email to desktop later

**If on Desktop:**
- You likely didn't use "Show original" / "View Source"
- Go back and follow proper extraction method
- See [Email Client Workflows](../workflows/email-clients.md) for instructions

---

### Notice: "Partial Analysis - Limited Data Available"

**Notice Message:**
```
ℹ️ Partial Analysis Notice

This analysis was performed on partial content. Missing: complete headers.

For more accurate results, provide complete email headers when possible.
Analysis confidence: Medium
```

**What It Means:**
- Some headers present but incomplete
- Not full body-only mode, but not complete either

**Common Scenarios:**
- Copied email from Properties dialog (Outlook) - headers only
- Forwarded email - loses original headers
- Email client provided partial source

**Solutions:**
1. Use proper "View Source" method for complete data
2. Accept medium confidence if complete source unavailable
3. Review SOC analyst report to see what data is available

---

### Notice: "Newly Registered Domain Detected"

**Notice Message:**
```
⚠️ Newly Registered Domain Detected

This email contains 1 domain registered less than 180 days ago.
Phishing attacks often use newly registered domains to avoid detection.

• suspicious-bank.com - 45 days old (Registrar: NameCheap)
```

**What It Means:**
- Domain in email is recently created
- Legitimate reason: New business, new marketing campaign
- Suspicious reason: Phishing campaign using disposable domain

**Is This a Problem?**
**Depends on context:**

**More Concerning When:**
- Combined with other red flags (failed auth, malicious URLs)
- Domain mimics known brand (paypa1.com vs paypal.com)
- Very new (<30 days)
- Free/cheap registrar (common in phishing)
- Email is unexpected or unsolicited

**Less Concerning When:**
- Known startup or new company
- Email is expected
- All other indicators are positive
- You have business relationship with sender

**Actions:**
1. **Don't dismiss** - newness alone is a warning sign
2. **Check other indicators** - risk score, authentication, external verification
3. **Verify through official channels** if requesting action
4. **Be extra cautious** with financial or credential requests

---

### Alert: "Externally Verified Threats"

**Alert Message:**
```
✅ Externally Verified Threats

2 malicious URL(s) confirmed by Google Safe Browsing, a database used by billions of
people worldwide to protect against phishing and malware.
```

**What It Means:**
- Major threat intelligence service confirmed malicious content
- **HIGH CONFIDENCE** - not just AI opinion, but verified threat
- Google, VirusTotal, URLhaus, or URLScan.io flagged URL(s)

**Is This a Problem?**
**YES** - This is critical confirmation:
- External services used by billions confirm threat
- AI and external verification agree
- Highest possible confidence in PHISHING verdict

**Actions:**
1. ❌ **DO NOT click any links** in the email
2. ❌ **DO NOT download attachments**
3. ✅ **DELETE immediately** after reporting
4. ✅ **Report to IT security** (work) or email provider
5. ✅ **Warn others** if email appears to come from known contact

---

## Performance Issues

### "Analysis is taking longer than expected"

**Normal Duration:**
- Desktop with headers: 10-20 seconds
- Mobile body-only: 8-15 seconds
- Very long emails: 20-30 seconds

**If Taking 30+ Seconds:**

**Possible Causes:**
1. Email contains many URLs (each verified against multiple services)
2. External API rate limits (during peak usage)
3. Large attachments being analyzed
4. Slow network connection

**Solutions:**
1. **Be patient** - system continues processing all layers
2. **Don't reload** - you'll lose progress
3. **Check progress indicator** - shows current step
4. **Wait up to 60 seconds** before considering it stuck

**If Truly Stuck (>2 minutes):**
1. Refresh page
2. Paste email again
3. Try again in a few minutes
4. Check internet connection

**Optimization Tips:**
- Analyze during off-peak hours if not urgent
- Body-only mode is faster if headers not critical
- Shorter emails process faster

---

### "Progress bar is not moving"

**What to Check:**
1. **Look at progress text** - bar may appear frozen but text updates
2. **Wait 10 seconds** - some steps take longer than others
3. **Check browser console** - press F12 to check for JavaScript errors

**Solutions:**
1. Let it run - appearances can be deceiving
2. If truly frozen for 2+ minutes, refresh and retry
3. Try different browser if problem persists

---

## Unexpected Results

### "Email marked LEGITIMATE but I'm sure it's phishing"

**Possible Reasons:**

**1. Sophisticated Phishing (False Negative)**
- Very convincing impersonation
- Compromised legitimate account (auth passes)
- Clean URLs that redirect later
- Zero-day campaign not yet in threat databases

**What to Do:**
- Review SOC analyst report in detail
- Check specific risk dimensions
- Look at confidence score (low confidence suggests uncertainty)
- **Trust your instincts** - if something feels wrong, verify through official channels
- Report as potential false negative

**2. Body-Only Mode Limitations**
- Analysis without headers has reduced capability
- Cannot check authentication (SPF, DKIM, DMARC)
- May miss IP reputation issues

**What to Do:**
- Analyze again from desktop with complete headers
- Check if blue "Body-Only Mode" warning appeared

**3. Legitimate Email with Unusual Characteristics**
- New marketing campaign (new domain)
- Poor email configuration (failed auth)
- Aggressive marketing language (urgency tactics)

**What to Do:**
- Verify through official channels (call company, login directly)
- Don't assume LEGITIMATE = safe for all actions
- Always verify unexpected financial requests

---

### "Email marked PHISHING but it seems legitimate"

**Possible Reasons:**

**1. False Positive**
- AI models overly conservative
- Legitimate email with some suspicious patterns
- Misconfigured email server (failed auth despite being real)

**What to Do:**
- Check confidence score (low = uncertain)
- Review SOC analyst report for specific findings
- Look at external verification - are URLs actually flagged?
- Verify sender through official channels
- Report as potential false positive

**2. Compromised Legitimate Account**
- Email IS from real account but account is hacked
- Authentication passes but content is malicious
- Behavioral analysis catches suspicious pattern

**What to Do:**
- Contact sender through different method (call, text)
- Ask if they sent the email
- Warn sender their account may be compromised

**3. Lookalike Domain**
- Domain very similar to legitimate (paypa1.com vs paypal.com)
- Easy to miss the difference

**What to Do:**
- Double-check domain spelling carefully
- Verify it exactly matches official domain
- If truly legitimate domain, email may still be phishing via compromised account

---

### "Risk score seems too high/low for the email"

**Understanding Risk Scores:**
- Scores are weighted across 5 dimensions
- One very high dimension can increase overall score
- External verification can override AI assessment

**If Risk Seems Too High:**

**Possible Reasons:**
1. One or two dimensions extremely high (e.g., failed auth + malicious URL = 85+)
2. Newly registered domain increasing score
3. Social engineering language detected
4. URL flagged by external service (major impact)

**What to Do:**
1. Review risk breakdown in SOC report
2. Check which dimensions are highest
3. Verify external verification results
4. Consider context (expected email, known sender, etc.)

**If Risk Seems Too Low:**

**Possible Reasons:**
1. Body-only mode (missing authentication checks)
2. No URLs to verify (text-only email)
3. Clean URLs + passed authentication despite suspicious content
4. Sophisticated phishing bypassing detection

**What to Do:**
1. Check confidence score (low confidence = uncertainty)
2. Review all risk dimensions
3. Don't rely solely on score - read findings
4. Verify unexpected requests regardless of score

---

### "Confidence is low (<60%) - What does this mean?"

**Low Confidence Indicators:**
- Mixed signals between layers (e.g., AI says phishing but URLs clean + auth passed)
- Body-only mode (missing data)
- Models disagree significantly
- Partial content
- Contradictory evidence

**What to Do:**
1. **Treat with caution** - system is uncertain
2. **Review SOC report** - understand the contradictions
3. **Manual review recommended** - don't automate actions
4. **Verify through official channels** before taking action
5. **Consider all factors**, not just verdict

**Example Scenarios:**
```
Low Confidence Scenario 1:
• Content Risk: 75 (AI thinks phishing)
• URL Risk: 10 (all URLs clean per Google/VirusTotal)
• Header Risk: 5 (SPF/DKIM/DMARC all passed)
→ Confidence: 58% (mixed signals)
→ Action: Verify - likely false positive

Low Confidence Scenario 2:
• Body-only mode (-15% confidence)
• Limited data available
→ Confidence: 52%
→ Action: Analyze from desktop for full confidence
```

---

## Mobile-Specific Issues

### "Can't paste email into Phishing Inspector on mobile"

**Solutions:**
1. **Long-press in text area** - paste option should appear
2. **Tap text area first** - ensure cursor is active
3. **Try different browser** - Chrome, Firefox, Safari
4. **Check clipboard** - may need to re-copy content
5. **Type a character first** - tap text area, type "a", then paste

---

### "Mobile analysis keeps showing errors"

**Common Issues:**
1. **Content too short** - need minimum 50-100 characters
2. **Only copied sender** - need body content too
3. **Special characters** - some emojis or formatting may cause issues

**Solutions:**
1. Copy more content (entire email body)
2. Include plain text version if available
3. Remove excessive emojis if present
4. Forward to desktop for complete analysis

---

### "Body-only mode but I want full analysis"

**Solution:**
Forward email to desktop and analyze there with complete headers.

**Steps:**
1. On mobile, forward suspicious email to yourself
2. Access forwarded email from desktop computer
3. Use "Show original" (Gmail) or "View Source" (Outlook)
4. Analyze with complete headers

**Note**: Forwarding preserves most (but not all) original headers.

---

## External Service Issues

### "Service shows 'Not configured' or 'Not checked'"

**What It Means:**
- Optional external API not configured
- Typically: VirusTotal, URLScan.io, AbuseIPDB (Google Safe Browsing is usually configured)

**Is This a Problem?**
**No** - Analysis continues with other available services:
- Google Safe Browsing (most critical) usually works
- Multiple other layers still check the email
- Verdict remains accurate

**Impact:**
- Slightly less comprehensive URL verification
- May miss some threats detected by disabled service
- Overall analysis still highly effective

---

### "All external services show 'Failed'"

**What It Means:**
- Network issues preventing API calls
- Rate limits exceeded (rare)
- Temporary service outages

**Is This a Problem?**
**Moderate** - External verification is important layer but not only layer:
- AI analysis still works (2 models)
- Email authentication still checked (if headers available)
- Behavioral analysis still works

**Solutions:**
1. **Try again in 5-10 minutes** - may be temporary issue
2. **Check internet connection** - ensure stable connection
3. **Accept limitations** - AI+auth can still detect many threats
4. **Manual verification** - check URLs yourself using VirusTotal.com

---

### "Google Safe Browsing shows 'Failed' but other services work"

**Impact:**
Google Safe Browsing is the highest-priority external service. If it fails:
- Still have VirusTotal, URLhaus, URLScan.io
- Analysis proceeds but with reduced external verification confidence

**Solutions:**
1. Verify manually: Visit [VirusTotal.com](https://www.virustotal.com) and check URLs
2. If other services flag URLs as malicious, trust them
3. Be more cautious with verdict if only AI detected phishing

---

## General Troubleshooting Steps

### Before Contacting Support

Try these steps in order:

1. **Refresh the page** and try again
2. **Clear browser cache** and cookies
3. **Try incognito/private browsing** mode
4. **Try different browser** (Chrome, Firefox, Safari)
5. **Check for browser extensions** - disable ad blockers temporarily
6. **Test with simple email** - verify system works with different content
7. **Check internet connection** - ensure stable network
8. **Review this guide** - solution may be documented above

---

## FAQ Quick Answers

**Q: Why is my analysis slow?**
A: Multiple external APIs checked for each URL (10-20 seconds normal).

**Q: Why body-only mode?**
A: No headers detected - normal for mobile. Forward to desktop for full analysis.

**Q: Can I trust low confidence results?**
A: Use caution - review full report and verify manually.

**Q: What if I disagree with verdict?**
A: Review SOC report details, check external verification, trust your instincts, verify through official channels.

**Q: Is analysis always accurate?**
A: No system is 100% - sophisticated attacks can evade detection. Always verify unexpected requests.

---

## Additional Resources

- **Getting Started**: [Getting Started Guide](../user-guides/getting-started.md)
- **Normal User Guide**: [Complete User Guide](../user-guides/normal-user-guide.md)
- **SOC Analyst Guide**: [Technical Guide](../user-guides/soc-analyst-guide.md)
- **Email Client Help**: [Email Client Workflows](../workflows/email-clients.md)
- **Quick Reference**: [Quick Reference Card](../user-guides/quick-reference.md)

---

**Still having issues?** Document the specific error, steps to reproduce, and email characteristics, then reach out through official support channels.
