# Task 7: DHL Express Courier - Complete Excel Macro Phishing Analysis

Analyzed a sophisticated DHL Express impersonation attack using Excel macro malware. Attack combines brand impersonation, geographic inconsistency, and multi-stage payload delivery. Demonstrates evolution from simple phishing links to full malware delivery chains.

### Email & Attachment Analysis

**Email Details:**
**Subject:** DHL Express Courier Shipping notice CBJ200620039539
**From:** DHL Express <info@glamcarcompany.de>
**Attachment:** Excel document.xlsx format

**Phishing Techniques Identified:**
1. **Spoofed Sender**: Display name "DHL Express" but domain is glamcarcompany.de. Legitimate DHL uses @dhl.com or @dhl.de only.

2. **Brand Impersonation**: HTML template mimics official DHL shipping notification with logos and tracking number CBJ200620039539 for credibility.

3. **Logistics Lure**: "Scheduled Shipment" theme exploits user expectation for package updates. High open rate category.

4. **Malicious Attachment**:.xlsx Excel file designed to trigger macro execution. Excel is preferred because "Enable Macros" prompt looks normal to users.

### Geographic Inconsistency Analysis

**Critical IOCs Found in Document:**
1. **Sender Domain**: German domain glamcarcompany.de
2. **Recipient Address**: "MENON AND MENON LIMITED, Warrimangar, KOLHAPUR" - Kolhapur is city in India
3. **Document Language**: Excel content entirely in Mandarin/Chinese

**Analysis:** German sender + Indian recipient + Chinese document = impossible business workflow. Geographic inconsistency is high-confidence phishing indicator.

**Document Content Observed:**
- Title: "供应商APPRISAL表格" = Supplier Appraisal Form in Chinese
- Fields: Name, Company office, Phone, Fax, Email, Establishment date, Owner/MD, Shareholders
- **Red Flag:** Single clickable "Hyperlink" present
- **Social Engineering:** "TO TRANSLATE LANGUAGE KINDLY CLICK ENABLE EDITING ABOVE" - tricks user into enabling macros

### Payload Execution Analysis

**Malware Details:**
**File Name:** regasms.exe
**Location:** C:\Users\admin\AppData\Roaming\regasms.exe
**Delivery Method:** Clicking hyperlink inside Excel downloads and attempts to execute regasms.exe

**Execution Behavior:**
Triggers "16 bit MS-DOS Subsystem" error - NTVDM CPU illegal instruction. Error confirms intent for direct code execution on victim machine. Payload failed in test environment but attack chain is proven.

**Attacker Objectives if Successful:**
1. **Establish Persistence**: Create backdoor or scheduled task to maintain access after reboot
2. **Exfiltrate Data**: Steal sensitive files, credentials, browser-stored passwords
3. **Deploy Ransomware**: Encrypt system and demand payment for recovery

### Complete Attack Chain
DHL Shipping Email → User opens Excel attachment → Excel prompts "Enable Editing" → User clicks Hyperlink → Downloads regasms.exe to AppData\Roaming → Attempts code execution → Establishes persistence/data theft

### L1 Analyst Workflow Applied
1. **Domain Verification**: glamcarcompany.de ≠ dhl.com = immediate flag
2. **Geographic Check**: Germany + India + China mismatch = impossible scenario
3. **Attachment Type**:.xlsx with hyperlink = abnormal. Real invoices are PDF static.
4. **Social Engineering**: "Enable Editing" instruction = bypass security warning tactic
5. **Payload Location**: AppData\Roaming\ execution = malware persistence location

### Key Learnings for SOC L1
1. **Geographic Consistency**: Legitimate companies maintain same locale across sender, recipient, and document language. Mismatch = phishing.

2. **Excel + Hyperlink Risk**:.xlsx files should not contain actionable links. Hyperlinks in Excel = malware delivery method.

3. **"Enable Editing" Trap**: Any instruction to bypass Office security warnings is malicious. Macros are blocked by default for a reason.

4. **AppData Persistence**: Malware installs to AppData\Roaming because users can write there without admin rights.

5. **Logistics Phishing Scale**: DHL, FedEx, UPS are top 3 impersonated brands due to expected shipping emails.

### Incident Response Playbook
If user interacted with this email:
1. **Do not open attachment or enable macros**
2. **If macros enabled**: Immediately disconnect device from network
3. **Hunt for regasms.exe**: Check C:\Users\[user]\AppData\Roaming\ for file presence
4. **Check Persistence**: Review Task Scheduler and Startup folder for malicious entries
5. **Full Scan**: Run EDR/Antivirus scan for malware and data exfiltration
6. **Block IOCs**: glamcarcompany.de domain, block.xlsx with external hyperlinks
7. **User Education**: Verify shipments directly at dhl.com, never via email attachment

### Why This Attack is Advanced
Combines 4 evasion techniques:
1. Brand impersonation for trust
2. Geographic confusion to distract analysis
3. Excel format to bypass.exe attachment filters
4. "Enable Editing" social engineering to defeat macro protection

### Evidence Screenshots
 Excel content showing Indian address + Chinese language + Hyperlink element
 MS-DOS error confirming regasms.exe execution attempt from AppData\Roaming
 <img width="1366" height="768" alt="Screenshot (29)" src="https://github.com/user-attachments/assets/d00340e7-16f7-4748-a747-e375418a728e" />

 <img width="1366" height="768" alt="Screenshot (30)" src="https://github.com/user-attachments/assets/fdc3e759-faed-4d4c-a3e9-a3568a2326a7" />



