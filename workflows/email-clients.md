# Email Client Workflows

Detailed step-by-step instructions for extracting complete email source from every major email client. For best analysis results, always provide complete email source with headers.

## Table of Contents
- [Why Complete Email Source Matters](#why-complete-email-source-matters)
- [Desktop Email Clients](#desktop-email-clients)
- [Web-Based Email](#web-based-email)
- [Mobile Devices](#mobile-devices)
- [Troubleshooting](#troubleshooting)

## Why Complete Email Source Matters

**Complete email source includes:**
- All email headers (Received, From, To, Subject, Date, etc.)
- Authentication results (SPF, DKIM, DMARC)
- Routing path (how email traveled through mail servers)
- Sending server IP addresses
- Email body (HTML and/or plain text)
- Attachments (encoded)

**Why headers are critical:**
- Verify sender authentication (detect spoofing)
- Check IP reputation (identify malicious infrastructure)
- Trace email routing (find origin)
- Validate email integrity (detect modification)

**Without headers:**
- Analysis limited to AI content analysis and URL verification
- Cannot check email authentication
- Cannot verify sender IP reputation
- Confidence reduced by 12-15%
- Higher chance of false negatives

---

## Desktop Email Clients

### Gmail Desktop (Web)

**Method 1: Show Original (Recommended)**

1. **Open the email** you want to analyze in Gmail
2. **Click the three-dot menu** (⋮) in the top-right corner of the email
3. **Select "Show original"** from the dropdown menu
4. A new tab opens showing the complete email source
5. **Option A - Copy to clipboard:**
   - Click the "Copy to clipboard" button at the top
   - Paste directly into Phishing Inspector
6. **Option B - Select all:**
   - Press `Ctrl+A` (Windows/Linux) or `Cmd+A` (Mac)
   - Press `Ctrl+C` (Windows/Linux) or `Cmd+C` (Mac)
   - Paste into Phishing Inspector

**What the source looks like:**
```
Delivered-To: yourname@gmail.com
Received: by 2002:a05:6402:3444:b0:52e:...
X-Google-Smtp-Source: ...
Authentication-Results: mx.google.com;
       dkim=pass header.i=@example.com
       spf=pass (google.com: domain of ...)
Received: from mail.example.com...
From: sender@example.com
To: yourname@gmail.com
Subject: Email Subject Here
Date: Wed, 15 Nov 2025 10:23:45 +0000
...
[Email body content follows]
```


**Method 2: Download Original**

1. Follow steps 1-4 above
2. Click "Download original" button
3. Save the `.eml` file
4. Upload the EML file directly to Phishing Inspector using the "EML File" tab

---

### Outlook Desktop (Windows/Mac)

**Method 1: View Source (Windows)**

1. **Open Outlook** desktop application
2. **Select the email** in your inbox (single click, don't open)
3. **Right-click** the email
4. **Select "View Source"** from context menu
5. A text editor opens with complete email source
6. **Press Ctrl+A** to select all
7. **Press Ctrl+C** to copy
8. Paste into Phishing Inspector

**Method 2: Properties (Windows)**

1. **Open the email** (double-click to open in new window)
2. **Go to File** menu → **Properties** (or Info → Properties)
3. In the Properties dialog, find **"Internet headers"** section at the bottom
4. **Select all text** in the Internet headers box
5. **Copy** (Ctrl+C) and paste into Phishing Inspector

**Note**: The Properties method only shows headers, not the body. To get complete source, use View Source method or export as MSG/EML.

**Method 3: Save as EML (Windows/Mac)**

1. **Select the email** in Outlook
2. **Go to File** → **Save As**
3. **Choose "Outlook Message Format - HTML" (.msg)** or export to EML if available
4. **Save the file**
5. Upload to Phishing Inspector via EML tab

---

### Outlook Web / Outlook.com

**Method 1: View Message Source (New Outlook Web)**

1. **Open the email** in Outlook on the web
2. **Click the three-dot menu** (...) in the top-right corner
3. **Select "View"** → **"View message source"** or **"View message details"**
4. A window opens with the complete email source
5. **Select all** (Ctrl+A / Cmd+A) and **copy** (Ctrl+C / Cmd+C)
6. Paste into Phishing Inspector

**Method 2: Message Details (Classic Outlook Web)**

1. **Open the email**
2. **Click the down arrow** next to the email subject/sender
3. **Select "Message details"** or **"View message source"**
4. Copy the displayed source


---

### Apple Mail (macOS)

**Method: View Raw Source**

1. **Open Apple Mail** application
2. **Select the email** you want to analyze
3. **Go to View menu** → **Message** → **Raw Source**
   - Or use keyboard shortcut: `Option + Command + U`
4. A new window opens showing complete email source
5. **Select all** (Cmd+A) and **copy** (Cmd+C)
6. Paste into Phishing Inspector

**Alternative: Save as EML**

1. **Select the email**
2. **Go to File** → **Save As**
3. **Choose format**: Raw Message Source (.eml)
4. **Save the file**
5. Upload EML file to Phishing Inspector

---

### Mozilla Thunderbird

**Method: View Source**

1. **Open Thunderbird**
2. **Select the email** in your inbox
3. **Press Ctrl+U** (Windows/Linux) or **Cmd+U** (Mac)
   - Or go to **View** → **Message Source**
4. A new window opens with complete email source
5. **Select all** (Ctrl+A / Cmd+A) and **copy** (Ctrl+C / Cmd+C)
6. Paste into Phishing Inspector

**Alternative: Save as EML**

1. **Right-click the email**
2. **Select "Save As"**
3. Save as EML file
4. Upload to Phishing Inspector

---

### Yahoo Mail (Web)

**Method: View Raw Message**

1. **Log into Yahoo Mail** (mail.yahoo.com)
2. **Open the email**
3. **Click "More"** (...) menu button
4. **Select "View Raw Message"**
5. A new window or panel opens with email source
6. **Select all** (Ctrl+A / Cmd+A) and **copy**
7. Paste into Phishing Inspector

---

### ProtonMail

**Method: View Source/Headers**

1. **Open ProtonMail** (mail.proton.me)
2. **Open the email**
3. **Click the three-dot menu** (...)
4. **Select "View source"** or **"View headers"**
5. Copy the displayed source/headers
6. Paste into Phishing Inspector

**Note**: ProtonMail's end-to-end encryption may limit some header information.

---

## Web-Based Email

### Generic Web Email Instructions

If your email provider isn't listed above, look for these options:

**Common menu options:**
- "View Source"
- "Show Original"
- "View Raw Message"
- "Message Source"
- "View Message Details"
- "View Headers"
- "View Internet Headers"

**Common locations:**
- Three-dot menu (...) or "More" menu
- View menu
- File menu → Properties
- Right-click context menu
- Settings or gear icon

**Steps:**
1. Open the email
2. Look for menu (usually three dots, gear icon, or "More")
3. Find "View Source", "Show Original", or similar option
4. Copy displayed source
5. Paste into Phishing Inspector

---

## Mobile Devices

### Important Note About Mobile

Most mobile email apps **do not provide easy access to complete email source with headers**. Mobile analysis uses "Body-Only Mode" which has limitations:

- ✅ AI content analysis still works
- ✅ URL verification still works
- ✅ Domain age checking still works
- ❌ Email authentication cannot be verified
- ❌ IP reputation cannot be checked
- ❌ Routing path cannot be traced

**Confidence reduced by 15%** due to missing header data.

### Mobile Workaround Options

**Option 1: Forward to Desktop (Recommended)**

1. On your mobile device, **forward the suspicious email** to yourself
2. Access the forwarded email from a **desktop computer**
3. Use **"Show original"** or **"View Source"** on desktop
4. Paste complete email source into Phishing Inspector

**Benefits**: Preserves most header information, allows full analysis

---

**Option 2: Body-Only Analysis (Limited)**

If you cannot access a desktop:

1. **Open the email** on your mobile device
2. **Long-press** to start text selection
3. **Drag selection handles** to select everything:
   - Sender information (if visible)
   - Subject line (if visible)
   - Complete email body
   - All links
4. **Tap "Copy"** or use **"Select All"** then **"Copy"**
5. Go to Phishing Inspector on mobile browser
6. **Paste** the copied content
7. System will automatically detect **Body-Only Mode** and show blue notice

**What to include:**
```
Try to copy text like this:

From: service@paypal.com
Subject: Verify your account

Dear Customer,

[Complete email body with all text and links]
...
```

**Tips:**
- Include "From:" line if you can see sender email
- Include "Subject:" line if visible
- Copy **everything** - don't edit or shorten
- Include footer text and signatures


---

### iOS (iPhone/iPad)

**Gmail App:**
1. Open email → Tap three-dot menu (⋮)
2. No "View Source" option available
3. Use **Body-Only Method** or **Forward to Desktop**

**Apple Mail App:**
1. Open email
2. No "View Source" available in mobile version
3. Use **Body-Only Method** or **Forward to Desktop**

**Yahoo Mail App:**
1. Open email → Tap "More"
2. No "View Raw Message" in mobile app
3. Use **Body-Only Method** or **Forward to Desktop**

**General iOS:**
- Most apps lack source view on mobile
- Best option: Forward to desktop or use body-only

---

### Android

**Gmail App:**
1. Open email → Tap three-dot menu (⋮)
2. No "Show original" option available
3. Use **Body-Only Method** or **Forward to Desktop**

**Outlook App:**
1. Open email
2. No "View Source" available in mobile app
3. Use **Body-Only Method** or **Forward to Desktop**

**General Android:**
- Mobile apps typically don't expose email source
- Best option: Forward to desktop or use body-only

---

## Troubleshooting

### "I can't find the View Source option"

**Check:**
1. Make sure email is open (not just selected)
2. Look in all menus: three-dot (...), "More", View menu, File menu
3. Try right-clicking the email (desktop only)
4. Search provider's help docs for "view email source" or "message headers"
5. If truly unavailable, use body-only mode or forward to different client

---

### "The source looks wrong or incomplete"

**If you see:**
```
From: sender@example.com
To: you@example.com
Subject: Subject line

[Body starts here immediately]
```

**Problem**: This is NOT complete source - missing headers (Received, Authentication-Results, etc.)

**Solution:**
- In Gmail, use "Show original" not "Forward"
- In Outlook, use "View Source" not "Properties" alone
- Ensure you copied everything from the source view window
- Check if you accidentally selected only part of the source

**Complete source should start like:**
```
Delivered-To: you@gmail.com
Received: by 2002:a05:...
X-Google-Smtp-Source: ...
Authentication-Results: mx.google.com;
       dkim=pass ...
       spf=pass ...
Received: from mail.example.com [IP]
...
From: sender@example.com
```

---

### "Should I use EML file or copy text?"

**Both work equally well** if EML contains complete source.

**Use EML file when:**
- Want to save emails for later analysis
- Analyzing multiple emails
- Provider offers easy EML export
- Want to preserve exact formatting

**Use copy/paste when:**
- Quick one-time analysis
- Provider makes copying easier than saving
- Mobile device (text copy only option)

---

### "Email source is huge (50+ pages)"

**This is normal** for emails with:
- Large email chains (many previous replies)
- Marketing emails with lots of tracking
- Multiple recipients
- Large attachments (base64 encoded)

**Don't worry:**
- Phishing Inspector handles long emails
- May take slightly longer to analyze (15-25 seconds)
- All content is necessary for accurate analysis

**Don't edit:**
- Copy entire source as-is
- Don't try to shorten or remove parts
- System handles long content automatically

---

### "Provider doesn't allow viewing source"

**Rare but possible.**

**Options:**
1. **Forward to different email account** (Gmail, Outlook.com) that allows source view
2. **Use body-only mode** (limited analysis better than no analysis)
3. **Contact provider support** - ask how to access full email source
4. **Change email provider** for better security tools

---

### "Analysis says body-only mode but I have headers"

**Possible causes:**
1. Headers incomplete (missing Received headers)
2. Only copied partial headers
3. Headers formatted incorrectly

**Solution:**
- Go back to email client
- Use official "View Source" / "Show Original" option
- Copy absolutely everything from the source window
- Don't manually type or reconstruct headers

---

## Best Practices Summary

### For Desktop Users

✅ **DO:**
- Use "Show original" (Gmail) or "View Source" (Outlook)
- Copy complete source including all headers
- Verify source starts with "Received:" or "Delivered-To:"
- Use EML file export if easier
- Analyze BEFORE clicking any links

❌ **DON'T:**
- Take screenshots (can't analyze images)
- Forward emails (loses original headers)
- Edit or shorten source
- Copy only the body
- Use Properties dialog alone (Outlook)

### For Mobile Users

✅ **DO:**
- Forward to desktop for complete analysis when possible
- Copy as much text as possible for body-only mode
- Include sender, subject, and complete body
- Accept body-only mode limitations for quick analysis

❌ **DON'T:**
- Expect full analysis from mobile
- Click links before analyzing
- Edit copied text
- Ignore body-only mode warnings

---

## Quick Reference Table

| Email Client | Desktop Method | Mobile Method |
|--------------|---------------|---------------|
| **Gmail** | Three-dot menu → Show original | Forward to desktop OR body-only |
| **Outlook Desktop** | Right-click → View Source | N/A (desktop only) |
| **Outlook Web** | Three-dot → View message source | Forward to desktop OR body-only |
| **Apple Mail** | View → Message → Raw Source (Opt+Cmd+U) | Forward to desktop OR body-only |
| **Thunderbird** | View → Message Source (Ctrl+U) | N/A (desktop only) |
| **Yahoo Mail** | More → View Raw Message | Forward to desktop OR body-only |
| **ProtonMail** | Three-dot → View source | Forward to desktop OR body-only |

---

## Additional Resources

- **Main Guide**: [Getting Started](../user-guides/getting-started.md)
- **Mobile Workflows**: [Mobile Devices Guide](./mobile-devices.md)
- **Troubleshooting**: [Common Issues](../troubleshooting/common-issues.md)
- **Quick Reference**: [Quick Reference Card](../user-guides/quick-reference.md)

---

**Need help with a specific email client not listed?** Check the provider's official documentation by searching: "[Provider name] view email source" or "[Provider name] view message headers"
