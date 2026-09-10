# Investigation Findings

## Finding 1 — Normal ICMP Traffic

The baseline capture showed normal ICMP communication between the Kali analyst machine and the Linux victim.

- Echo Request: Kali → Linux Victim
- Echo Reply: Linux Victim → Kali
- ICMP Type 8: Echo Request
- ICMP Type 0: Echo Reply

**Assessment:** Normal network activity.

---

## Finding 2 — Exposed SSH Service

Nmap identified TCP port 22 as open on the Linux victim.

- Port: `22/tcp`
- Service: SSH

SSH is a legitimate remote administration service, but it should be monitored for unusual authentication attempts and unexpected connections.

**Assessment:** Service exposed; requires monitoring.

---

## Finding 3 — Exposed HTTP Service

Nmap identified TCP port 80 as open.

- Port: `80/tcp`
- Service: HTTP

A web service can be a potential attack surface and should be investigated further during a security assessment.

**Assessment:** Service exposed; requires further investigation.

---

## Finding 4 — TCP Connection Behavior

Wireshark analysis confirmed the TCP three-way handshake:

`SYN → SYN/ACK → ACK`

TCP reset (`RST/ACK`) traffic was also observed.

**Assessment:** TCP connection establishment and termination behavior successfully identified.

---

## Overall Assessment

The investigation established a baseline of normal network traffic and identified two exposed services on the Linux victim.

No confirmed malicious activity was identified from the traffic analyzed so far.

Further investigation can focus on SSH authentication activity, HTTP requests, and abnormal connection patterns.
