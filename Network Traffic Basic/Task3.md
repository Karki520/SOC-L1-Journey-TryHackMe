# Network Traffic Basics 

---

### Application & Transport Layer Analysis

#### Application Layer
On the application layer we can find two important information structures depending on which application layer protocol is used:
1. **Application header information** - metadata about the communication
2. **Application data itself (payload)** - actual content being transferred

**HTTP Example - Logs vs Packets:**
Most web proxies and firewalls log only header data. They don't log the content/payload.

**GET Request Headers:**
Client is requesting file named `suspicious_package.zip`.

**Server Response Headers:**
200 status code means request was accepted.

**Key Limitation:** Logs can't show the content of the ZIP file highlighted as payload. Only packet capture reveals the actual binary data being transferred.

#### Transport Layer
Application data and header are segmented and encapsulated at transport layer into smaller pieces. Each piece includes a transport header, usually TCP or UDP.

**Firewall Logs:**
Firewall logs include source/destination ports and flags, but miss other fields. Still valuable for detecting attacks like session hijacking.

**Wireshark TCP Analysis - Session Hijacking Detection:**
- **Lines 1-3:** Normal TCP 3-way handshake
- **Lines 4-5:** Legitimate data transfer  
- **Anomaly:** Line 6 shows Seq=34567232 suddenly far apart from previous sequence numbers. This indicates possible session hijacking and warrants further investigation.

#### Key Takeaways
1. **Application Layer:** Headers show what file was requested/downloaded, but payload shows what was actually inside. NTA needed to inspect malicious ZIP content.
2. **Transport Layer:** Firewall logs show basic TCP metadata, but packet analysis of sequence numbers is required to detect session hijacking.
3. **Logs = Metadata, Packets = Full Story:** Headers and logs help with initial detection, but packet capture is mandatory for complete analysis.

---

### Internet & Link Layer Analysis

#### Internet Layer
When transport layer sends a segment, internet layer adds IP header. If segment > Maximum Transmission Unit (MTU), it gets fragmented. Each fragment gets its own IP header.

**Key Fields for Security Analysis:**
1. **Source/Destination IP** - Basic tracking
2. **TTL** - Detect routing issues  
3. **Fragment Offset** - Position of fragment in original packet
4. **Total Length** - Size of fragment
5. **More Fragments (MF) Flag** - Indicates more fragments coming

**Fragmentation Attack Example:**
Attackers use tiny fragments or overlapping byte ranges to evade IDS or mess up reassembly.
