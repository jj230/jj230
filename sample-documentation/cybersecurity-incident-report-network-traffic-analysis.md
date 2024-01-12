---
description: Created during Google's Cybersecurity Course based on fictional information
---

# Cybersecurity Incident Report:  Network Traffic Analysis

### Logs:

13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)

13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2&#x20;

udp port 53 unreachable length 254\


13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)

13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2&#x20;

udp port 53 unreachable length 320



13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)

13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2&#x20;

udp port 53 unreachable length 150

### &#x20;Summary of the problem found in the DNS and ICMP traffic log

The network protocol analyzer logs indicate that port 53 is unreachable when attempting to access yummyrecipesforme.com. Port 53 is normally used for DNS requests. UDP protocol was used. This may indicate a problem with the DNS server or could be indicative of a malware attack, specifically a denial of service attack.&#x20;

### Analysis of the data and one solution to implement

Customers first reported being unable to reach the website and receiving the message, “udp port 53 unreachable.” The network security team attempted to access the website at 13:24, 13:26, and 13:28 today, but received the same message. They analyzed the logs and discovered that port 53, which is used for DNS traffic, was unreachable. We are continuing to investigate the root cause of this problem to determine how to restore access to the website. Our next steps are to see if the DNS server is down or if there is a misconfiguration in a firewall that is blocking access to port 53.
