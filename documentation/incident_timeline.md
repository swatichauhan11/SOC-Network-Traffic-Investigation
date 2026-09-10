# Incident Timeline

## 1. Baseline Network Activity

A baseline network capture was analyzed to understand normal communication between the Kali machine and the Linux victim machine.

- Kali IP: `192.168.100.10`
- Linux Victim IP: `192.168.100.20`
- Capture file: `normal-ping.pcap`
- Protocol observed: ICMP

The capture contained ICMP Echo Request packets from Kali to the victim and ICMP Echo Reply packets from the victim back to Kali.

This represented normal ping communication and no intentionally generated suspicious activity was identified in the baseline capture.

---

## 2. Network Scanning Activity

An Nmap scan was performed against the Linux victim machine to identify accessible services.

The scan identified:

- `22/tcp` — SSH
- `80/tcp` — HTTP

These open ports were recorded as potential investigation points because network services can provide entry points that should be monitored in a SOC environment.

---

## 3. TCP Connection Analysis

TCP traffic was examined in Wireshark to understand the connection establishment process.

A successful TCP three-way handshake was observed:

1. Kali → Linux Victim: `SYN`
2. Linux Victim → Kali: `SYN, ACK`
3. Kali → Linux Victim: `ACK`

This confirmed that a TCP connection was successfully established.

TCP reset traffic (`RST/ACK`) was also observed during the investigation and was studied to understand how TCP connections can be terminated or rejected.

---

## 4. Investigation Summary

The investigation progressed from establishing a normal network baseline to identifying exposed services and analyzing TCP communication.

The main observations were:

- Normal ICMP communication was successfully identified.
- SSH and HTTP services were discovered through Nmap.
- TCP three-way handshake behavior was analyzed in Wireshark.
- TCP reset behavior was also observed.
- Zeek deployment was attempted but deferred due to installation issues.

These observations form the foundation for further SOC-style network traffic investigation.
