# Task 3 - Email Delivery & Email's Journey
**Room:** phishingemails1tryoe  
**Status:** Complete

## What I learned today
Emails feel instant, but there's a whole system moving them behind the scenes. 3 protocols + 6 steps = how every email reaches inbox. For SOC, this matters because phishing emails also follow this same path. If I know the normal path, I can spot when attacker breaks it.

## Part 1: The 3 Protocols

**SMTP - Simple Mail Transfer Protocol**  
Job: Sends emails from sender to mail server  
Think: Postman who picks up your letter and takes it to post office  
Port: 25, 587, 465

**POP3 - Post Office Protocol**  
Job: Downloads emails to one device only  
Key points:
- Emails stored on single device after download
- Sent messages stay only on device you sent from  
- Emails usually deleted from server after download
Think: Old postbox - you take letter, it's gone from post office
Problem for us: Evidence disappears. Hard for L1 to investigate later.

**IMAP - Internet Message Access Protocol**  
Job: Syncs emails across all devices  
Key points:
- Emails stay on server
- Can download to multiple devices - phone + laptop same inbox
- Sent messages stored on server
- Messages remain unless you delete them
Think: Google Drive - same file everywhere
Better for SOC: We can pull headers/attachments from server even after user reads mail.

## Part 2: An Email's Journey - 6 Steps

1. **User sends email**  
   Sender's client uses SMTP to push message to their mail server

2. **Mail server queries DNS**  
   Sending server asks DNS: "What's the mail server for gmail.com?"  
   DNS is Internet's phonebook

3. **DNS responds**  
   DNS returns MX record with recipient mail server address

4. **Email is delivered**  
   Message travels across Internet to recipient's server  
   Each hop adds a `Received` header - this is where we catch spoofing

5. **Recipient checks mailbox**  
   User's email client connects to mail server via IMAP or POP3

6. **Email is retrieved**  
   Downloaded via POP3 or synced via IMAP to user's device

## Why this matters for phishing analysis
Every email must pass through steps 1-4. Attackers can fake the `From` address, but they can't easily fake the `Received` chain. 

When I analyze `email1.eml` next, I'll read those `Received` headers from bottom to top and match them with these 6 steps. If a hop is missing or server name looks fake, that's our red flag.

Companies use IMAP now because POP3 deletes evidence. Good retention policy = easier for SOC team.


## Next
Opening `email1.eml` now. Will check `From`, `Reply-To`, and `Received` headers to see if this phishing sample breaks the normal journey.
