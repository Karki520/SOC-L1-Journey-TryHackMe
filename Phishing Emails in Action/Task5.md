# Task 5: Netflix ID Suspended 

### Campaign Overview
Analyzed a Netflix billing phishing campaign that uses malicious PDF attachment instead of direct links. This shows how attackers evolved to bypass URL-based email filters by hiding malicious links inside attachments.

### Email Header Analysis
**Subject:** Netllx ID Suspended
**From:** Netllx billing <z99@musacombi.online>
**BCC:** Present with @yahoo.com address

**Red Flags in Header:**
1. **Brand Misspelling**: "Netllx" instead of "Netflix" in both subject and display name. Deliberate typo to evade brand filters.
2. **Domain Mismatch**: Actual sender domain is musacombi.online. Legitimate Netflix emails only come from @netflix.com or @account.netflix.com.
3. **BCC Usage**: BCC field present indicates mass mailing campaign. Attackers hide recipient list to avoid detection.

### Email Body Analysis
**Main Message:** "Your account is on hold" + "Please update your payment details"

**Tactics Used:**
1. **Artificial Urgency**: Account suspension warning creates panic. User fears losing Netflix access and clicks without verification.
2. **Billing Issue Lure**: "Trouble with your current billing information" is most common phishing theme for subscription services.
3. **Brand Impersonation**: Uses Netflix logo and HTML styling to mimic official billing notifications. Visual copy increases trust.

### Attachment Analysis
**File:** Payment-update.pdf [37KB]

**Why Attackers Use Attachments:**
1. Email security filters scan URLs more aggressively than attachments
2. Users perceive PDFs as safer than clicking direct links
3. PDF can contain embedded JavaScript or hyperlink to malicious site
4. Bypasses basic link scanning at email gateway

**Risk:** PDF contains embedded link titled "Update Payment Account" that redirects to non-Netflix domain for credential harvesting.

### Additional Indicators Identified
1. **Atypical Phone Number Format**: Footer contains phone number with unusual formatting. Netflix does not provide phone support in automated billing emails.

2. **Spoofed Help Center Reference**: Email mentions "help.netflix.com" to build false sense of legitimacy. However, sender domain does not match, confirming spoofing.

3. **Generic Greeting**: Uses "Hello Customer" instead of account holder's actual name. Legitimate Netflix emails personalize with account name.

4. **Dual Call-to-Action**: Both "Update Payment Account" button and text link present. Increases probability of user clicking.

### Attack Chain Mapped
Email with urgency → User opens PDF attachment → PDF contains "Update Payment Account" link → Redirect to fake Netflix login page → Credentials stolen

### L1 Analyst Workflow Applied
1. **Step 1 - Header Check**: Verified sender domain musacombi.online ≠ netflix.com
2. **Step 2 - Subject Analysis**: Flagged urgency + account suspension keywords
3. **Step 3 - Brand Verification**: Noticed "Netllx" misspelling in display name
4. **Step 4 - Attachment Risk**: Identified PDF as delivery method instead of direct link
5. **Step 5 - Content Review**: Found generic greeting and spoofed help center reference

### Key Learnings for SOC L1
1. **Attachment!= Safe**: PDF, DOCX, ZIP files can deliver phishing links or malware. Never open unexpected attachments.
2. **Brand Typos Matter**: "Netllx" vs "Netflix" is simple but effective filter evasion. Always check spelling.
3. **Domain is Truth**: Logos and design can be copied. Only sender domain cannot be faked.
4. **Urgency = Red Flag**: Any email threatening account suspension or service interruption needs extra scrutiny.

### Incident Response Actions
If end user reports interaction with this email:
1. Advise immediate deletion without opening attachment
2. If attachment was opened: disconnect device, run full antivirus scan
3. Reset Netflix password if credentials were entered on linked page
4. Block sender domain musacombi.online at email gateway
5. Add rule to quarantine emails with "billing" + PDF attachment from non-netflix.com domains

<img width="1366" height="768" alt="Screenshot (27)" src="https://github.com/user-attachments/assets/48def89f-7d89-469a-927a-d71caafdb8ea" />
