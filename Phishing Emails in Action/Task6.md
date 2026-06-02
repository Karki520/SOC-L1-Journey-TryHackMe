# Task 6: Your Recent Purchase - Apple BCC Phishing with .dot Attachment & Redirect

Analyzed an advanced Apple Support impersonation attack. Email uses blank body, BCC recipient method, and .dot Word template attachment containing embedded malicious redirect. This demonstrates evolution from link-based to attachment-only phishing with redirector chains.

### Email Header & Delivery Method Analysis

**Email Details:**
**Subject:** Re: Action Required - Your recent purchase "Double Jackpot Slots Las Vegas" on the App Store - Date: Fri 03 Apr 2020 09:32:24 +0000
**From:** Apple Support <donoreply-storemailsedmopzl07zo7o9@sumpremed.com>
**Recipient:** BCC

**Phishing Techniques Identified:**
1. **Spoofed Display Name**: Shows "Apple Support" but domain is sumpremed.com. Legitimate Apple uses @apple.com or @email.apple.com only.

2. **BCC Recipient Method**: User placed in BCC instead of To field. Attackers use BCC to hide recipient list and mass mail campaigns while appearing personal.

3. **Artificial Urgency**: Subject uses "Action Required" + fake unauthorized purchase. Triggers panic about fraudulent transaction.

4. **Fake Purchase Lure**: "Double Jackpot Slots Las Vegas" App Store purchase mentioned. Gambling + unexpected charge = high emotional response.

5. **Typos in Headers**: Room notes spelling errors in From and To addresses. Additional indicator of malicious origin.

6. **Blank Email Body**: No text content at all. Forces user to open attachment for details. Bypasses text-based spam filters.

### Attachment & Redirect Analysis

**Attachment:** Double Jackpot... .dot file - Microsoft Word Template format

**Why .dot is Dangerous:**
1. Word Template files can contain auto-executing macros
2. Unusual format for purchase receipt. Legitimate Apple receipts are PDF
3. Can contain embedded objects and images with malicious links

**Malicious Redirect Chain Found:**
Image inside .dot document contains embedded link:
`https://t.tumblr.com/redirect?z=https://apps.ios-games.mansiiea.com/?njhdhw10d&t=...`

**URL Breakdown:**
1. **Redirector Usage**: Uses t.tumblr.com to mask final destination from email filters
2. **Fake Domain**: apps.ios-games.mansiiea.com - not owned by Apple. Real Apple domains: apple.com, icloud.com
3. **Obfuscation**: Excessive length and random parameters to evade pattern detection
4. **Keyword Stuffing**: Includes "apps" and "ios" to appear legitimate to user

**Fake Receipt Content:**
Document image shows fake App Store receipt with:
- Apple ID: example@appleid.com
- Order ID: MN HLSF 45X G  
- Product: Double Jackpot Slots Las Vegas, $14.99
- Apple Card promo to add credibility

### Complete Attack Chain
Blank Email → User opens .dot attachment → Fake receipt image displayed → User clicks image/link → Redirect through tumblr.com → Lands on fake Apple ID login page → Credentials stolen

### L1 Analyst Workflow Applied
1. **Recipient Check**: BCC = immediate flag. Legit companies use To field for billing.
2. **Sender Verification**: sumpremed.com ≠ apple.com. Domain mismatch confirmed.
3. **Body Analysis**: Blank body is suspicious. Legit emails always contain text.
4. **Attachment Type**: .dot file for receipt = wrong format. High risk category.
5. **URL Analysis**: Redirector + long random parameters + non-Apple domain = malicious.

### Key Learnings for SOC L1
1. **BCC Usage**: Legitimate billing emails never use BCC. Always To field with user email visible.
2. **Blank Body Tactic**: Absence of content is itself an indicator. Attackers hide from keyword detection.
3. **Attachment Format Risk**: .dot, .docm, .xlsm = macro-enabled formats. Higher risk than PDF.
4. **Redirector Chains**: Attackers use tumblr.com, bit.ly to hide final malicious URL from scanners.
5. **Visual Deception**: Fake receipts inside documents look authentic with order IDs and dates.

### Incident Response Actions
If user interacted with this email:
1. Do not open .dot attachment. Delete email immediately
2. If opened: Disconnect device, do not enable macros if Word prompts
3. Run full antivirus/EDR scan for macro malware
4. Reset Apple ID password if credentials entered on fake page
5. Block sumpremed.com and apps.ios-games.mansiiea.com at email gateway
6. Create rule to quarantine emails with .dot attachments + "purchase" keywords

### Key Differentiator from Previous Tasks
Task 4-5 used visible links or PDF attachments. Task 6 shows:
- No email body text at all
- BCC delivery method
- Malicious link hidden inside document image
- Multi-stage redirect through tumblr.com

This shows attacker adaptation to improve evasion.

### Evidence Screenshots
1. Email header showing spoofed Apple Support and BCC delivery
2. Attachment analysis showing .dot file and embedded malicious redirect URL

<img width="1366" height="768" alt="Screenshot (28)" src="https://github.com/user-attachments/assets/6ae097ae-2473-423d-9e6c-6c53fdb67817" />
