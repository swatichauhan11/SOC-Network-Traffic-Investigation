# Investigation Timeline

## 1. Baseline Network Activity

A baseline packet capture was analyzed to understand normal communication between the Kali analyst machine and the Linux victim machine.

* Kali IP: `192.168.100.10`
* Linux Victim IP: `192.168.100.20`
* Capture file: `normal-ping.pcap`
* Protocol observed: ICMP

The capture showed normal bidirectional ping communication:

```text
Kali → Linux Victim: ICMP Echo Request (Type 8)
Linux Victim → Kali: ICMP Echo Reply (Type 0)
```

No intentionally suspicious activity was identified during the baseline phase.

---

## 2. Network Service Discovery

Nmap was used to identify network-accessible services on the Linux victim machine.

The scan identified:

| Port | Protocol | Service |
| ---- | -------- | ------- |
| 22   | TCP      | SSH     |
| 80   | TCP      | HTTP    |

The exposed services were recorded as investigation points because network-accessible services can increase the attack surface of a host.

---

## 3. TCP Connection Analysis

The discovered services were examined at the packet level using Wireshark.

A TCP three-way handshake was observed:

```text
Kali → Linux Victim: SYN
Linux Victim → Kali: SYN, ACK
Kali → Linux Victim: ACK
```

This confirmed successful TCP connection establishment.

TCP `RST/ACK` packets were also observed during the investigation. These packets were analyzed to understand TCP connection rejection and termination behavior.

---

## 4. SSH Authentication Investigation

SSH authentication activity was examined using the Linux victim's authentication logs.

Repeated failed authentication attempts were observed, including attempts involving the username `wronguser`.

Relevant observations included:

| Time     | Event                             |
| -------- | --------------------------------- |
| 13:56:03 | Failed SSH authentication attempt |
| 13:56:07 | Failed SSH authentication attempt |
| 14:13:42 | Connection closed by invalid user |

The authentication activity was documented as security-relevant because repeated failed SSH authentication attempts can warrant further investigation in a real SOC environment.

**Assessment:** Suspicious authentication activity was observed, but no system compromise was established from the available evidence.

---

## 5. HTTP Traffic Investigation

HTTP communication was analyzed to understand normal client-server behavior.

The investigation included:

* HTTP GET requests
* HTTP server responses
* TCP connections associated with the HTTP service
* HTTP response codes

The traffic was reviewed to establish expected HTTP behavior and provide a baseline for identifying abnormal requests in future investigations.

---

## 6. Investigation Summary

The investigation progressed through the following workflow:

```text
Baseline Traffic
       ↓
Nmap Service Discovery
       ↓
TCP Packet Analysis
       ↓
SSH Authentication Review
       ↓
HTTP Traffic Analysis
       ↓
Security Findings
```

The investigation identified:

* Normal ICMP communication
* Exposed SSH and HTTP services
* TCP three-way handshake behavior
* TCP reset behavior
* Repeated failed SSH authentication attempts
* Normal HTTP client-server communication

No confirmed system compromise or malicious activity was established from the available evidence.

This investigation demonstrates a basic SOC workflow of establishing a network baseline, identifying exposed services, analyzing network traffic, reviewing authentication activity, and documenting security-relevant findings.
