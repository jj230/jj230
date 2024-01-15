# Cybersecurity Incident Report: Website Redirection

Created during Google's Cybersecurity Course. Based on the fictional dns & http log at the bottom of this page. 

### Technical Answers

| Section 1: Identify the network protocol involved in the incident                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| In this incident, the network protocol involved is HTTP at the application layer. By analyzing the logs, it can be seen that the problem is a redirection to a new site, which is done through HTTP.  |

| Section 2: Document the incident                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| The website yummyrecipesforme.com is directing customers to download malware and then redirecting them to a spoof website that shows all of the recipes for free. Customers have written in to tell us this information. Our security team has been investigating this incident and found that this is happening to all users who are trying to access the website. Upon further investigation, the website’s source code has been altered by someone who performed a brute force attack on an admin’s password.  |

| Section 3: Recommend one remediation for brute force attacks                                                                                                                                                                                                                              |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Our security team recommends enforcing 2FA for administration accounts. With 2FA, even if a password is discovered through brute force, a malicious actor will not be able to gain entry into an account because they won’t have the ability to verify the login with the second factor.  |

### Non-Technical Summary

An attacker changed our website so that it would end up directing people to a fake version of our website that shows all of our recipes for free. We are now losing money as customers can get our product for free.&#x20;

The attackers were able to change our website because they guessed one of our admin passwords.&#x20;

To prevent a loss of income and an attack like this in the future, our security team is recommending enforcing 2FA for administration accounts. 2FA will mean that even if someone finds out a password, they will be unable to get it. While this is less convenient for those with an admin account, it will help save money, reputational harm, and future attacks.&#x20;

[Google Cybersecurity Course Document](https://docs.google.com/document/d/1HXXgABNANaS0TFe_HiI7QtTamv3AgMGhyqka1SVv3Eg/edit?resourcekey=0-z2vZuYGIo37C3lOdccPfag&usp=sharing)
*Written by Google as part of their Cybersecurity Course*

