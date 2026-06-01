# Task 4 - Email Header Analysis 
**Room**: phishingemails1tryoe  
**Status**: Complete

## What I learned today
The body can lie, but headers don't. An attacker can fake the email content and write "Microsoft Security Alert" to scare you. But they can't hide their real IP and fake server in the headers. That's why L1 analysts always check headers before reading the body.

## Part 1: Email Structure
Every email has 2 main parts:

**1. Email Header - The metadata part**
Users don't see this in normal view. You get it from "View Source". It contains:
- From: Sender's address
- To: Receiver's address  
- Reply-To: Where replies actually go
- Subject: Subject line
- Date: When it was sent
- Received: Full path of servers it passed through

**2. Email Body - The message content**
This is plain text or HTML. Links, images, attachments live here.

Users get scared reading the body. Analysts catch attackers by reading headers.

## Part 2: Key Header Fields in email1.eml

From the screenshot sample header:

**1. From**: Sender's email address  
`ADT Security Services <newsletters@ant.anki-tech.com>`  
Display name says ADT, but domain is `ant.anki-tech.com`. Real ADT uses `adt.com`. Classic typosquatting.

**2. To**: Receiver's email address  
`alexa@yahoo.com`  
The target user.

**3. Reply-to**: Where replies go  
`reply@ant.anki-tech.com`  
Biggest red flag! From shows ADT but replies go to a random domain. No legit company does this.

**4. Subject**: Email subject line  
`Help protect your budget by protecting your home`  
Fear + urgency tactic. "Protect your budget or else..." - standard phishing style.

**5. Date**: When email was sent  
`12/21, 15:25`  
Important for timeline. SOC teams track when incidents happened.

## Part 3: How to View Raw Headers - Message Source
Email clients only show 5 fields by default. For real analysis you need raw source.

**In Thunderbird:**
1. **Menu method**: View → Message Source
2. **Shortcut**: `Ctrl + U` - faster, this is what SOC analysts actually use

Open raw source and you get all technical data hidden from normal view.

## Part 4: What Raw Headers Reveal
Message Source shows extra details:

**1. Originating IP Address**  
Found in `Received: from [IP]` line. Example: `86.222.142.150`  
This tells you where the email really came from. From field can say Microsoft, but IP might be from Russia. Game over.

**2. Full Header Details**  
- `Sender`: Actual account that sent it
- `DKIM Signature`: Whether email was authenticated
- `SPF Result`: Whether sender was authorized
- `Received Chain`: Complete path through all servers

<img width="1366" height="768" alt="Screenshot (19)" src="https://github.com/user-attachments/assets/f5a4312c-f12d-4ea2-b2bf-62986dbe5b03"
  />

  <img width="1366" height="768" alt="Screenshot (20)" src="https://github.com/user-attachments/assets/b97dd42c-7109-4f4f-82d2-eb679d8e3f26" />


