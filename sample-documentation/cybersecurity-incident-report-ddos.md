---
description: Created during Google's Cybersecurity Course based on fictional information
---

# Cybersecurity Incident Report: DDoS

Based on a fictional TCP/HTTP log included at the bottom of this page.

#### Technical Answers

| Identify the type of attack that may have caused this  network interruption                                                                                                                                                                                                                                                                        |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The TCP log shows over 100 SYN requests in under a minute from the IP Address 203.0.113.0. The web server 192.0.2.1 seems to be experiencing a DoS attack, specifically through the malicious actor utilizing a SYN flood. The flood of SYN requests is overwhelming the web server, making it unresponsive to all requests, even legitimate ones. |

| Explain how the attack is causing the website to malfunction & potential consequences                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The flood of SYN requests is overwhelming the web server, making it unresponsive to all requests, even legitimate ones. If the web server remains unresponsive, the company could suffer damages to its reputation and finances. Customers may lose trust in the safety of the website or they may simply not want to wait for it to get back online. In either case, customers may decide to give their business to a different company. |

#### Non-Technical Answers

| Identify the type of attack that may have caused this  network interruption                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Our website, just like physical highways, can only handle so much traffic at a time before there's a traffic jam. It appears that someone is purposely sending extra traffic to our website to try to shut it down. Our website is overwhelmed by the number of requests. |

| Explain how the attack is causing the website to malfunction & potential consequences                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Our website has too many cars on its highways, so to speak, so traffic is unable to move in or out. No one can access our website and our website can't respond to anyone. If our website continues to remain inaccessible, customers may start to form a negative opinion of our company or simply may not want to wait until we are back online again. They may take their business elsewhere, hurting the company financially. |

{% embed url="https://docs.google.com/spreadsheets/d/1VkkFlFpBInQsJ-sTH6Zhi7CYnB1lCDGkyJ1F_bflJz0/edit?usp=sharing" %}
Written by Google as part of their Cybersecurity Course
{% endembed %}
