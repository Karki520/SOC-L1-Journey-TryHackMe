

### Full Packet Capture

When the logs don't provide enough information, we must dig deeper. To do so, we need to correlate logs, inspect full packet captures, and check network statistics.

**How to Capture Packets - 2 Options:**
1. **Install a physical network tap**
2. **Configure port mirroring**

#### Network Tap
A network tap is a physical device placed inline in the network. 

**Key Features:**
1. **Creates copy** of all network traffic that passes without affecting performance
2. **Copied data** forwarded to packet capture box, IDS, or monitoring system via dedicated monitoring port
3. **Operates at Link Layer** of TCP/IP model - copies electrical/light signals
4. **No IP/MAC needed** - operates below Layer 3, so no address required
5. **Zero delay** - no added latency to network traffic

**Use Case:** Best for permanent, high-reliability packet capture. Hardware TAPs like ProfiShark ensure 100% traffic visibility without switch dependency.

#### Port Mirroring / SPAN
Port mirroring is a software approach to copying packets from one port on an intermediary device to another port attached to IDS, packet capture box, or monitoring system.

**Vendor Names:**
- **Cisco:** SPAN - Switched Port Analyzer
- **Other vendors:** RSPAN, ERSPAN, port mirror

**Cisco SPAN Configuration Example:**
```cisco
Switch(config)# monitor session 1 source interface fastEthernet0/1
Switch(config)# monitor session 1 destination interface fastEthernet0/2
