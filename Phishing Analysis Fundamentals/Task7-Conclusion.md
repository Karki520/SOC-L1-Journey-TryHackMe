# TryHackMe - Phishing Emails | Task 7 - Conclusion

**Room Completed**: Phishing Analysis Fundamentals  


---

### What I Actually Learned in This Room

Finally finished the first phishing room. Started from zero and now I can actually look at a suspicious email without panicking.

**Journey of this room:**

1. **Task 2 - Email Address**: Learned how email addresses are structured. `user@domain.com` - local part vs domain part. Attackers spoof domain to look legit. `microsof.com` instead of `microsoft.com`

2. **Task 3 - Email Delivery**: How email travels from sender to receiver. SMTP, MX records. Basic but important to understand where it can go wrong.

3. **Task 4 - Email Headers**: This was new for me. `From`, `To`, `X-Originating-IP`, `Received` fields. Found that X-Originating-IP thing by searching in email source. Had to defang it before pasting.

4. **Task 5 - Email Body**: Looked at HTML source of email body. Found hidden links and fake buttons. Hovering over links is now a habit.

5. **Task 6 - Types of Phishing**: Spam, Phishing, Spear, Whaling, Smishing. Whaling for CEOs was interesting. Also learned about defanging URLs - `http://` → `hxxp[://]` so no one clicks by accident.

6. **Task 7 - Conclusion**: Wrapping up. Room taught me the technical basics + how to think like an attacker.

---

### My 3 Biggest Takeaways

1. **Headers don't lie, but From field does**: Anyone can fake the "From" address. Real info is in headers, especially `Received` chain and `X-Originating-IP`.

2. **Urgency is a red flag**: "Account locked in 24 hours", "Verify now". Attackers use panic so you don't think. If email creates urgency, I stop now.

3. **Defanging is basic hygiene**: Learned to never share raw IPs/URLs in notes or reports. `192.168.1.1` → `192[.]168[.]1[.]1`. Small habit, big safety.

---

### Next: Business Email Compromise (BEC)

Room ended with a note about BEC. That's when attacker hacks a real company email and tricks employees to transfer money. No malware, no fake link - just trust. 

Sounds scarier than normal phishing. Need to read more about this next.

---



**Status**: Task 7 Complete ✅ Room Done  


---
*Note to self: 7 day streak going. Don't break it. Consistency > Speed.*
