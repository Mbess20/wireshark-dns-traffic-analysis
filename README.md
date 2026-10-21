# Wireshark DNS Traffic Analysis

## Project Overview
This project documents a hands-on network traffic investigation performed using Wireshark on macOS. The objective was to capture network traffic, examine DNS queries and responses, analyze DNS resolution, and identify DNS error responses.

## Lab Environment
- Operating System: macOS
- Analysis Tool: Wireshark
- Network Interface: Wi-Fi (en0)
- Capture Format: PCAPNG
- Traffic Source: Local network capture

## Objectives
1. Capture and inspect live network traffic.
2. Identify DNS queries and corresponding responses.
3. Examine DNS resource records and IP address resolution.
4. Measure DNS response times.
5. Identify DNS error responses.
6. Document observations and security relevance.

## Methodology
1. Captured network traffic using Wireshark on the Wi-Fi interface.
2. Applied the display filter `dns` to isolate DNS and mDNS traffic.
3. Applied `dns.flags.response == 1` to identify DNS responses.
4. Selected packet 221 and expanded the Domain Name System response details.
5. Matched the response with its original request, packet 217.
6. Applied `dns.flags.rcode != 0` to identify nonzero DNS response codes.

## Findings
| Observation | Result |
|---|---|
| Total packets captured | 2,790 |
| DNS/mDNS packets displayed with dns filter | 56 |
| DNS response packet | 221 |
| Corresponding DNS request | 217 |
| Transaction ID | 0xa7d7 |
| Response time | 45.77 ms |
| DNS record type | A (IPv4) |
| Answer records | 8 |
| DNS response status | No error |
| Nonzero DNS response codes observed | 0 |

### DNS Resolution
A DNS query requested an IPv4 address for an Apple-related service domain. The DNS server returned eight A records. Wireshark correlated the response to the original request using transaction information.

### DNS Error Analysis
The display filter `dns.flags.rcode != 0` returned no matching packets in the capture. No nonzero DNS response codes were observed in the captured traffic.

## Security Relevance
DNS analysis can support security operations by helping analysts identify:
- Unusual or unexpected domain lookups
- Repeated failed DNS queries
- Potential command-and-control communication patterns
- DNS configuration and connectivity problems

No confirmed malicious DNS activity was identified during this limited investigation. Additional traffic, context, and threat intelligence would be required for a security determination.

## Skills Demonstrated
- Network packet capture
- Wireshark display filtering
- DNS protocol analysis
- IPv4 and IPv6 fundamentals
- Packet correlation
- Network troubleshooting
- Technical investigation documentation

## Future Improvements
- Compare DNS A and AAAA records.
- Analyze TCP connection establishment.
- Examine TLS traffic and encrypted communications.
- Add sanitized packet screenshots.
- Perform additional controlled network traffic investigations.

## Privacy
Raw packet captures are not published because they may contain sensitive network identifiers and traffic metadata.
