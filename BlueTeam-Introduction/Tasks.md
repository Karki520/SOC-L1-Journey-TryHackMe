# Security Analyst Journey Intro

### What I learned today

**1. What does a SOC Analyst actually do?**
SOC = Security Operations Center. Basically the 24x7 security team of any company. 
As L1, my job is to sit and watch the alerts coming in. Most alerts are false alarms, 
so I need to check quickly and close them. If something looks real, I escalate it to L2.

Main tasks: Check SIEM dashboards, read cyber news, triage alerts, stop small breaches before they become big.

**2. SOC Team Structure - Who does what**
This was confusing at first but now it makes sense:
- **L1 - Me:** First person to see alerts. Fast triage, close false positives, escalate real ones.
- **L2 / Will:** Senior guy. If I get stuck, I ask him. He handles complex cases I can't solve.
- **SOC Engineer / Corey:** He doesn't look at alerts. He builds and maintains the tools - SIEM, Firewall, EDR.
- **SOC Manager / Emily:** She manages the whole SOC team and reports to management.
- **Incident Responder / Daniel:** Only called when shit hits the fan. Ransomware, full breach etc.

**L1 Daily stuff:** Checking for data stealers, analyzing phishing mails, helping with ransomware alerts, 
writing basic detection rules with L2.

**3. Lab Part**
Had to go through the alert dashboard and find the malicious IP. 
Found it after scrolling through a bunch of noise.

**Lab Answers:**
- Malicious IP: 221.181.185.159 
- Escalated to: Will Griffin - because he's L2/Senior Analyst
- Flag after blocking IP on firewall: THM{until-we-meet-again}

**Workflow I followed:** Alert came → checked IP → looked malicious → escalated to Will → blocked IP on firewall → got flag

### Tools used
TryHackMe AttackBox, Alert Dashboard, basic SIEM navigation

### Screenshots for proof

<img width="1366" height="768" alt="SIEM dashboard" src="https://github.com/user-attachments/assets/6079a83d-6e12-4b1c-88b0-ac53b9dee219" />


<img width="1366" height="768" alt="IP Hunter" src="https://github.com/user-attachments/assets/d5f68f1d-b237-4688-9f9e-b702b0666a7d" />


<img width="1366" height="768" alt="Firewall Block" src="https://github.com/user-attachments/assets/bed6aa5d-5f45-456e-883a-c41bd08eabcb" />



