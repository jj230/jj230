---
description: Created during Google's Cybersecurity Course based on fictional information
---

# Cybersecurity Incident Report: Website Redirection

Based on [fictional dns & http log](https://docs.google.com/document/d/1HXXgABNANaS0TFe\_HiI7QtTamv3AgMGhyqka1SVv3Eg/edit?usp=sharing\&resourcekey=0-z2vZuYGIo37C3lOdccPfag).

| Section 1: Identify the network protocol involved in the incident                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| In this incident, the network protocol involved is HTTP at the application layer. By analyzing the logs, it can be seen that the problem is a redirection to a new site, which is done through HTTP.  |

| Section 2: Document the incident                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The website yummyrecipesforme.com is directing customers to download malware and then redirecting them to a spoof website that shows all of the recipes for free. Customers have written in to tell us this information. Our security team has been investigating this incident and found that this is happening to all users who are trying to access the website. Upon further investigation, the website’s source code has been altered by someone who performed a brute force attack on an admin’s password.  |

| Section 3: Recommend one remediation for brute force attacks                                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Our security team recommends enforcing 2FA for administration accounts. With 2FA, even if a password is discovered through brute force, a malicious actor will not be able to gain entry into an account because they won’t have the ability to verify the login with the second factor.  |
