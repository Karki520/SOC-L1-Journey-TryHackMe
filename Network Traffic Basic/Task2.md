 # Task 1-2: Why Should We Analyse Network Traffic

### Purpose of Network Traffic Analysis
We use network traffic analysis to monitor network performance, check for abnormalities in the network like sudden performance peaks or slow network, and inspect the content of suspicious communication internally and externally such as exfiltration via DNS, download of a malicious ZIP file over HTTP, and lateral movement.

### SOC Perspective
From SOC perspective network traffic analysis helps in detecting suspicious or malicious activity, reconstructing attacks during incident response, and verifying and validating alerts to reduce false positives.

### DNS Tunneling and Beaconing Case Study
**Scenario:** SOC analyst receives alert that host WIN-016 with IP 192.168.1.16 is sending unusual number of DNS queries to same TLD using different subdomains.

**DNS Logs from Firewall:**
2025-10-03 09:15:23 SRC=192.168.1.16 QUERY=aj39skdm.malicious-tld.com QTYPE=A
2025-10-03 09:15:31 SRC=192.168.1.16 QUERY=msd91azx.malicious-tld.com QTYPE=A  
2025-10-03 09:15:45 SRC=192.168.1.16 QUERY=cmd01.malicious-tld.com QTYPE=TXT
2025-10-03 09:15:45 SRC=192.168.1.16 QUERY=cmd01.malicious-tld.com QTYPE=TXT

**What Logs Can Tell Us:**
From DNS logs we can retrieve query and querytype, subdomain and top-level domain which can be checked on abuseDB or VirusTotal to see if domain is malicious, host IP to identify system sending queries, destination IP to verify if IP is flagged malicious using AbuseIPDB or VirusTotal, and timestamp to build timeline mapping out suspicious queries.

**Limitation of Logs:**
DNS logs don't contain more information than metadata, so it is hard to draw conclusion based on logs alone. We need to inspect DNS traffic more thoroughly and check content of DNS queries and replies to determine nature of these queries and replies. Threat actors use DNS tunneling and beaconing to hide C2 commands because firewalls register queries and responses but not payload.

### Additional Real Scenarios
1. **Malicious HTTP Download:** Based on logs for an end-user system, the system began to deviate from normal behavior around 4 PM UTC. Analyzing network traffic going to and from this system we found a suspicious HTTP request and were able to extract a suspicious ZIP file for malware analysis.
2. **DNS Exfiltration:** We received an alert that an end-user system is sending many DNS requests in comparison to baseline of the network. After inspecting the DNS requests we discovered data was being exfiltrated using a technique called DNS tunneling.

### Key Takeaway
Logs show when and what metadata was accessed. Packets show what actually happened inside the traffic. NTA bridges this gap and is mandatory to detect attacks like DNS tunneling and C2 beaconing that bypass firewall rules. Now that we know why we need network traffic analysis, the next task covers what exactly we can monitor.


