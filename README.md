# SOC-Network-Traffic-Investigation
A hands-on SOC lab for capturing, analyzing, and investigating network traffic using Wireshark, tcpdump, Zeek, and Splunk.
## Project Status

This project demonstrates a practical SOC-style investigation of network traffic in a controlled virtual lab environment.

### Completed Investigations

- ICMP baseline traffic analysis
- Nmap service discovery
- SSH service identification
- HTTP service investigation
- TCP three-way handshake analysis
- TCP RST/RST-ACK analysis
- Wireshark packet analysis
- Investigation findings and timeline documentation

### Key Findings

The investigation established normal network behavior and identified exposed SSH and HTTP services on the Linux victim machine.

No confirmed malicious activity was identified in the traffic analyzed.

### Tools Used

- Kali Linux
- Wireshark
- Nmap
- Linux
- VirtualBox
- GitHub

### Documentation

Detailed investigation notes are available in the `documentation/` directory:

- `incident-timeline.md`
- `network-analysis.md`
- `findings.md`

### Future Improvements

- Add Zeek-based network monitoring
- Analyze authentication logs
- Investigate HTTP request patterns in greater depth
- Add simulated suspicious traffic
- Develop detection rules and SOC alerts
