### Email Body - Text vs HTML

**What I saw**:  
Left side plain text email: "Hello Dave, send Q1 finance report". Right side HTML email with red "URGENT: CLOUD ACCESS SUSPENDED" banner.

**Key takeaway**:  
Emails can be plain text or HTML. HTML allows styling, images, links. Phishers use HTML to make fake urgency banners that look real. 

**Lesson**:  
Don't trust what you see. Rendered view can hide the real structure. Always check raw source.

---

###  Viewing HTML Source Code

**What I saw**:  
Side-by-side comparison of "Rendered HTML" vs "Raw HTML". Rendered view shows clean email. Raw HTML shows all tags, links, and embedded content.

**Key takeaway**:  
Raw source reveals stuff the rendered view hides. You can see actual URLs, hidden images, and suspicious code. Thunderbird blocks images by default - that's why raw source matters.

**Lesson**:  
If an email asks you to "click here", check raw HTML first. The link text might say `netflix.com` but href could be `bit.ly/malicious123`.

---

### Reconstructing Attachments - Headers

**What I saw**:  
Explanation of 3 headers for attachments:
1. **Content-Type: application/pdf** - tells file type
2. **Content-Disposition: attachment; filename="..."** - tells it's an attachment + filename  
3. **Content-Transfer-Encoding: base64** - tells encoding method

**Key takeaway**:  
Attachments aren't just "attached". They are encoded as text inside email body. Headers tell us how to decode them.

**Lesson**:  
Random filename like `zmqpalgh.pdf` is a red flag. Legit companies use proper names like `Invoice_2025.pdf`.

---

###  Raw HTML with Base64 Data

**What I saw**:  
Left: Rendered view showing PDF attachment icon. Right: Raw HTML with `Content-Type`, `Content-Disposition`, and huge base64 string starting with `JVBERi0xLjY...`

**Key takeaway**:  
That long base64 string IS the PDF file. It's just encoded as text so email can transfer it. Decode it and you get the original file back.

**Lesson**:  
`JVBERi` at start = PDF file signature in base64. Same way `UEsDB` = ZIP file. Attackers hide malware in base64.

<img width="1366" height="768" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/d38e1fcd-e6df-4f05-9d23-cdea72bbd4ee" />


---

###  Questions + Answers

**Questions asked**:
1. Content-Type of attachment? → `application/pdf` 
2. Name of attachment? → `zmqpalgh.pdf`  
3. Hidden flag value? → `THM{BENIGN_PDF_ATTACHMENT}` 

**How I got the flag**:  
1. Copied base64 string from email source
2. Used CyberChef → From Base64 recipe  
3. Output started with `%PDF-1.6` so decode worked
4. Saved output as `zmqpalgh.pdf` 
5. Opened PDF → Found `THM{BENIGN_PDF_ATTACHMENT}` inside

   <img width="1366" height="768" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/3c229323-c4d0-4efc-94a9-53a76696b17e" />


**Final lesson**:  
Attackers can hide files + flags inside base64. Always reconstruct attachments in sandbox. Never open directly on main system.

---

