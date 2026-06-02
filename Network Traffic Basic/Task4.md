# Task 4: Network Traffic Sources and Flows


### Traffic Classification
Practically, it's more helpful to focus on specific sources and flows instead of just TCP/IP theory. A corporate network typically has predetermined network flows and sources.

**Traffic Sources - 2 Categories:**
1. **Intermediary** - Devices through which traffic mostly passes
2. **Endpoint** - Devices where traffic originates and ends

**Traffic Flows - 2 Categories:**
1. **North-South**: Traffic that exits or enters the LAN and passes the firewall. Internet-bound traffic.
2. **East-West**: Traffic that stays within the LAN, including LAN that extends to the cloud. Internal traffic.

### Sources

#### Intermediary Sources
Devices through which traffic mostly passes. While they generate some traffic, it's significantly lower than what endpoint devices generate.

**Examples:** Firewalls, switches, web proxies, IDS, IPS, routers, access points, wireless LAN controllers, and ISP infrastructure.

**Traffic Types from Intermediaries:**
1. **Routing protocols**: EIGRP, OSPF, BGP
2. **Management protocols**: SNMP, PING
3. **Logging protocols**: SYSLOG  
4. **Supporting protocols**: ARP, STP, DHCP

**Key Point:** Intermediary devices generate less traffic but provide critical visibility into network health, routing, and control plane attacks.

#### Endpoint Sources
Devices where traffic originates and ends. Endpoint devices take the bulk of the network bandwidth.

**Examples:** Servers, hosts, IoT devices, printers, lab machines, cloud resources, mobile phones, tablets, and more.

**Key Point:** Endpoints consume most bandwidth and are primary targets for malware, data exfiltration, and lateral movement.

### Flows

A network traffic flow is typically determined by the services available in the network, such as Active Directory, SMB, HTTPS, and so on.

#### North-South Traffic
NS traffic is often monitored closely as it flows from the LAN to the WAN and vice versa.

**Characteristics:**
1. Passes through firewall - key visibility point
2. Has two streams: ingress (inbound) and egress (outbound)
3. Most well-known services: HTTPS, DNS, SSH, VPN, SMTP, RDP, and many more

**Security Importance:** Configuring firewall rules and logging properly are key to visibility. This is where perimeter security tools focus.

#### East-West Traffic
EW traffic stays within the corporate LAN, so it is often monitored less. However, it is important to keep track of these flows.

**Security Importance:** When the network is compromised, an attacker will often exploit different services internally to move laterally within the network.

**East-West Service Categories:**
1. **Directory, Authentication & Identity Services** - AD, LDAP, Kerberos
2. **File shares & print services** - SMB, NFS, printing
3. **Router, switching, and infrastructure services** - STP, HSRP, VRRP
4. **Application Communication** - Internal APIs, microservices
5. **Backup & Replication** - Database replication, backups
6. **Monitoring & Management** - SNMP, SYSLOG, monitoring agents

**Key Takeaway:** East-West traffic is critical for detecting lateral movement. Most breaches move internally after initial compromise, making EW monitoring essential.

### Key Takeaways
1. **Source Focus**: Intermediaries = control plane traffic, Endpoints = data plane traffic
2. **Flow Focus**: North-South = perimeter security, East-West = internal/lateral movement detection
3. **SOC Relevance**: Both source types and flow types need monitoring. Attackers often enter via NS but move via EW.
