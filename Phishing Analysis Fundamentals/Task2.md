# Task 2 - The Email Address 
**Status:** Complete

## What I learned today
Every phishing investigation starts with the email address itself. If I don't understand how it's built, I'll miss the clues attackers hide in plain sight.

## Anatomy of an Email Address
Email addresses follow a simple structure: `username@domain.com`

1. **Username**: The mailbox name. This identifies the specific user on the mail server. Example: `david` in `david@tryhackme.com`
2. **@ Symbol**: Separates username from domain. Introduced by Ray Tomlinson on ARPANET in the 1970s. Tells the system where to route the email.
3. **Domain Name**: The mail server responsible for receiving the message. Example: `tryhackme.com`

## Simple analogy that stuck with me
Think of an email address like a home mailing address:
- **Domain** = Street or apartment building. It gets the mail to the right location.
- **Username** = Specific person or mailbox number inside that building.

Without both parts, the mail server has no idea where to deliver the message.

## Why this matters for phishing
Attackers use tricks in both parts:
- Fake domains: `microsft.com` instead of `microsoft.com` 
- Fake usernames: `security-team` instead of real employee names
- Display name spoofing: Shows "CEO" but actual email is `random@gmail.com`

If I can't break down the address, I can't spot the spoof.

## Screenshot proof

 <img width="1366" height="768" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/dd3188f1-368d-438f-b8ac-d10948779458" />

