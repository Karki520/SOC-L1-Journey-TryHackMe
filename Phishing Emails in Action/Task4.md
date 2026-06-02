# Task 4: Download Document Here - Complete Phishing Chain Analysis
### Campaign Summary
Analyzed a complete multi-stage phishing attack chain. Attack starts with a fake document email and ends with a credential harvesting page. This demonstrates how attackers use multiple redirects and brand impersonation to bypass security filters.

### Stage 1: Initial Phishing Email
**Subject:** RE: Claim #:HBD-4636 |+ FSG Realty Holdings LLC | HBD100396391 6/25/20  
**From:** Nir Barak <nrb@profitly.com>

**Indicators of Compromise:**
1. **Artificial Urgency**: Email states "Expires July 15, 2021" with same-day expiration to pressure quick action
2. **Brand Impersonation**: Uses Citrix/document sharing theme to appear legitimate
3. **Single Call-to-Action**: Only "Download Document Here" button present to force user interaction
4. **Sender Domain Mismatch**: Display name shows Citrix context but actual domain is profitly.com

### Stage 2: Fake OneDrive Landing Page
After clicking the download button, user is redirected to a fake OneDrive page.

**Red Flags:**
1. **Malicious URL**: URL is not onedrive.live.com. Labeled as "Shady URL" in analysis
2. **Visual Impersonation**: Uses OneDrive logo and PDF icon to build user trust
3. **Fake Interface**: "View Document" button does not open a real document

**Attacker Goal**: Establish initial trust using a well-known brand before moving to the next redirect.

### Stage 3: Fake Adobe Login Portal
Clicking "View Document" on the fake OneDrive page redirects to an Adobe impersonation page.

**Red Flags:**
1. **Malicious URL**: Not adobe.com. Second "Shady URL" in the chain
2. **Poor Grammar**: Page contains nonsensical wording and grammatical errors
3. **Credential Selection**: Offers multiple "Sign in with email provider" options to target any user

**Attacker Goal**: Get user to select their email provider, then show a matching fake login page.

<img width="1366" height="768" alt="screenshot" src="https://github.com/user-attachments/assets/f18ea6ab-df1f-4549-a025-06c55920a6ec" />


### Stage 4: Fake Outlook Credential Harvesting Page
Final destination of the redirect chain is a fake Microsoft Outlook login page.

**URL:** http://bdkmotorsport.com/wp-duua

**Critical Indicators:**
1. **Wrong Domain**: bdkmotorsport.com is an automotive website, not Microsoft. Legitimate Outlook login only occurs on outlook.com or microsoft.com
2. **No HTTPS**: Uses HTTP instead of HTTPS. Legitimate Microsoft services always use HTTPS with valid certificates
3. **Credential Theft Mechanism**: Page does not authenticate users. Even with valid credentials, it always returns "Invalid Credentials" error while sending credentials to attacker server

### Attack Techniques Identified
1. **Multi-Stage Redirect Chain**: Uses 3-4 redirects to evade email security filters that only check the first URL
2. **Brand Chaining**: Sequentially impersonates Citrix → OneDrive → Adobe → Microsoft to increase perceived legitimacy
3. **Time Pressure**: Same-day expiration creates urgency to bypass user critical thinking
4. **Credential Harvesting**: End goal is stealing email and password combinations
5. **AI-Generated Content**: Room notes that grammatical errors are becoming less reliable as an indicator because attackers now use AI to generate polished phishing content

### Key Learnings for L1 Analysis
1. **URL/Domain Verification**: Always check the actual URL in the address bar, not logos or page design
2. **HTTPS Validation**: Legitimate Microsoft/Google/Adobe pages always use HTTPS with valid certificates
3. **Redirect Analysis**: More than one redirect in a document sharing workflow is a major red flag
4. **Login Context**: Real document sharing services do not require login on a third-party domain to view files

### Incident Response Notes
If a user reports entering credentials on such a page:
1. Force immediate password reset
2. Enable Multi-Factor Authentication if not already enabled
3. Review account activity for unauthorized access

   
