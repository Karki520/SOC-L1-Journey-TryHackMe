 #Types of Phishing 

**What I learned**: Email is still the #1 entry point for attacks. Attackers use social engineering to make us click.

**5 Types of malicious emails:**
1. **Spam/Malspam**: Bulk junk mail. "You won iPhone!" Malspam = spam + malware attached.
2. **Phishing**: Fake company emails. Pretend to be bank/Netflix to steal password.
3. **Spear Phishing**: Targeted attack. They know your name, company, job role. Way more convincing.
4. **Whaling**: Spear phishing for big fish - CEO, CFO. Goal is money transfer or sensitive data.
5. **Smishing**: SMS phishing. "Your parcel is stuck, track here" with malicious link.

**My thought**: The more personal it gets, the more dangerous it is. Spam < Phishing < Spear < Whaling.
---

### Anatomy of a Phishing Email

**What makes phishing emails work**: Attackers use same tricks again and again.

**6 Red flags I noted:**
1. **Spoofed From**: `noreply@microsof.com` - Missing 't' in microsoft. Domain spoofing.
2. **Urgency**: "Account locked in 24 hours" - Creates panic so you don't think.
3. **Brand Impersonation**: Exact logo + colors of legit company to build trust.
4. **Grammar Issues**: "Dear costomer" type mistakes. AI se kam ho gaye but awkward phrasing still there.
5. **Generic Content**: "Dear Customer" instead of your name. Mass mail ka sign.
6. **Hidden Links**: `bit.ly/secure-login` - Text me legit URL dikhayenge, link kahi aur jayega.

**Lesson I wrote down**: If email has urgency + asks for creds + link looks weird = 99% phishing. Stop and verify.

---

###  Anatomy Continued + Safe Analysis

**2 more tricks attackers use:**
1. **Hidden/Shortened Links**: `bit.ly/secure-login` hides real destination. Always hover before clicking.
2. **Malicious Attachments**: `invoice.pdf.exe` - Double extension trick. Windows hides .exe, shows only .pdf.

**Safe Analysis - Defanging**:
Analysts never share raw URLs/IPs in reports. We "defang" them so no one clicks by accident.

**Rule:**
- `@` → `[@]`
- `.` → `[.]` 
- `http` → `hxxp`
- `://` → `[://]`

**Example from room:** `http://www.suspiciousdomain.com` → `hxxp[://]www[.]suspiciousdomain[.]com`

**Why it matters**: One accidental click during investigation = whole lab compromised.

---

 Investigation Task

**Practical part starts here**

Task: Analyze `email3.eml` in VM and answer:
1. Which reputable organization is being spoofed?

**How I plan to check:**
1. Open email3.eml in Thunderbird/Notepad
2. Check `From:` field - kaunsi company ban rahe hai
3. Check subject line - "Your PayPal account suspended" type hint dega
4. Check body for logo/name mention

**Defanging habit I picked up:**
Before posting any IOC in Git/report, defang first. Safety first.

**Status**: Task 6 Complete 
