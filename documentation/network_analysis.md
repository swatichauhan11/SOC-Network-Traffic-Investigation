# Network Traffic Analysis

## Environment

| Machine | IP Address | Role |
|---|---|---|
| Kali Linux | 192.168.100.10 | Analyst / Attacker |
| Linux Victim | 192.168.100.20 | Target |

## ICMP Baseline Analysis

The baseline capture `normal-ping.pcap` was analyzed in Wireshark.

The traffic consisted of ICMP Echo Request and Echo Reply packets.

### Observed Flow

`Kali → Linux Victim: ICMP Echo Request (Type 8)`

`Linux Victim → Kali: ICMP Echo Reply (Type 0)`

This indicates normal bidirectional ping communication between the two systems.

No intentionally suspicious activity was identified in the baseline capture.

## Nmap Service Discovery

An Nmap scan was performed against the Linux victim.

The following TCP ports were found open:

| Port | Protocol | Service |
|---|---|---|
| 22 | TCP | SSH |
| 80 | TCP | HTTP |

These services were recorded for further investigation.

## TCP Handshake Analysis

Wireshark was used to analyze TCP connection establishment.

The following three-way handshake was observed:

1. `SYN` — Kali initiated the connection.
2. `SYN, ACK` — Linux Victim acknowledged the request.
3. `ACK` — Kali acknowledged the response.

This represents a successful TCP connection establishment.

TCP `RST/ACK` packets were also observed and analyzed to understand connection termination or rejection behavior.

## SOC Relevance

From a SOC analyst perspective, these observations demonstrate the importance of establishing a normal traffic baseline and then identifying deviations from expected behavior.

Open services such as SSH and HTTP should be monitored for unusual connection attempts, repeated failures, scanning activity, or other anomalous patterns.
