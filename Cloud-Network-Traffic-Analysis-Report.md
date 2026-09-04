# Cloud Network Traffic Analysis Report — My Solution

For this project, I took the DNS, TCP, ICMP, and TLS findings from my Wireshark capture and mapped each one to the cloud security control that would catch or reveal the same activity on AWS or Azure. The concept is simple: what Wireshark shows on a local machine, a cloud platform should show at the network level through logs instead of a packet capture.

## Methodology
I started from my local Wireshark capture (filtered by DNS, TCP, HTTP, and TLS), pulled out the behaviors worth flagging, and asked: *"If this same traffic happened inside a VPC or Azure VNet, what log or security control would show it to me?"*

## Findings Mapped to Cloud Controls

| What I Found on the Wire | Cloud Equivalent | Why It Matters |
| :--- | :--- | :--- |
| **DNS Query / Response Pairs** (Standard A-record resolution to public IPs) | **Route 53 Resolver Query Logs** (AWS) / **Azure Firewall DNS Proxy Logs** | Plain VPC Flow Logs do not capture domain names—only IP addresses. To see which domains are being resolved inside a cloud network, DNS-specific query logging is required. |
| **ICMP Traffic / Port Unreachable Packets** | **AWS VPC Flow Logs (`REJECT` records)** / **Azure NSG Flow Logs (`Action: Deny`)** | A rising count of rejected flows against a target destination reveals scanning behavior or misconfigured routing rules, flagging potential reconnaissance. |
| **TCP 3-Way Handshake (`SYN`, `SYN-ACK`, `ACK`)** | **AWS VPC Flow Logs (`ACCEPT` records)** & **Security Group Evaluation** | Tracking connection establishment allows cloud security engineers to verify whether inbound traffic successfully traversed Network Security Groups (NSGs) or hit a blocked state. |
| **Unencrypted HTTP Traffic (Port 80)** | **AWS WAF / Application Load Balancer (ALB) Access Logs** | Unencrypted traffic on port 80 lacks confidentiality. In the cloud, edge security controls should flag or redirect plaintext traffic to secure HTTPS channels. |
| **Encrypted TLS Handshake & Cipher Suites (Port 443)** | **AWS CloudTrail / Azure Monitor / TLS Termination Logs** | While packet contents remain hidden behind ciphertext, edge gateways and load balancers log handshake metadata, certificate validation states, and client cipher selections. |

## Conclusion
Translating local Wireshark packet analysis to cloud telemetry bridges the gap between low-level network troubleshooting and cloud security monitoring. Understanding how raw packet states translate into VPC flow logs, DNS query logs, and NSG rule evaluations is essential for detecting threats in modern cloud infrastructure.
