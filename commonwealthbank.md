### Tools/Skills: 
SIEM (Splunk), Dashboard Creation, Data Analysis, Data Visualization, Fraud-Related Data

---

# Commonwealth Bank: Cybersecurity Job Simulation

# Overview

<div align="left" data-full-width="false">

<img src="" width = 700>

</div>
<br>

## Task 1: Fraud Data Analysis - Splunk Dashboard Creation
"Analyze and visualize cyber data to uncover trends and patterns."

The company asked for a dashboard that would help gather necessary data to predict or detect fraud. They were specifically interested in the following categories: merchants, age of customers, gender of customers, category of purchases and month of purchase. Based on the specific charts the company indicated they'd like to have, I designed a dashboard in splunk for easy visualization of this data.
<br>
<br>
![Screenshot 2024-02-21 at 11 59 17 AM](https://github.com/jj230/jj230/assets/93885534/b82caf83-30c5-49a2-984f-27d9a6094b4f)
<br>

## Task 2: Incident Response
"Mitigate cyber incidents by analyzing, responding and recovering for your organization."

IT Services at Commonwealth Bank has flagged an issue that my team must fix. The incident includes staff complaints and a possible network compromise.
<br> <br>
### *Timeline of Events*
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/19b61512-228b-4bab-8966-df305e2289d6" width = 500>
</div>
<br> <br>

### *Incident Response Plan*
#### Attack Identification
<div align="left" data-full-width="false">
  
<img src="https://github.com/jj230/jj230/assets/93885534/6cb1c101-7465-4040-8e4d-859c7dba2aba" width = 600>
</div>

#### Initial Steps
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/fe6cbad9-80ed-4f8a-9688-55e92cfebd39" width = 600>
</div>

#### Containment Steps
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/88b3f6e0-4370-4059-b0cf-863aef8f79dc" width = 600>
</div>

#### Resolve Steps
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/7e6de076-d193-494b-aa40-4893fd63ad0b" width = 600>
</div>

#### Recovery Steps
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/427917f5-f206-4296-929a-6b5db755a9f6" width = 600>
</div>

#### Post-Incident Steps
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/d08f910c-fe04-4cb3-9c43-1273b4edf4d5" width = 600>
</div>


## Task 3: Raise Security Awareness - Infographic
Based on [guidance given by the Australian Cyber Security Centre (ACSC)](https://www.cyber.gov.au/protect-yourself/securing-your-accounts/passphrases/creating-strong-passphrases), I created an infographic for using passphrases instead of passwords. While this may not have prevented the phishing email, it's an easy way to increase employee awareness of being safer in general. Additionally, the more employees think about their digital safety, the less likely they will be to fall for a phishing email.

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/9bf93dd2-c78f-4c88-afca-dcfe23010d9a" width = 300>
</div>

## Task 4: Web Application Security - Pen Testing

### Executive Summary
This report details the results of a penetration testing challenge that was completed to identify vulnerabilities in the "Basic" web challenge from HackThisSite.org. The results show critical vulnerabilities that allow unauthorized access to all areas in the /basic/ section. This could lead to financial, reputational, and customer loss for an organization. Recommendations for remedying this vulnerabilities are given.

### Vulnerabilities Overview
Injection
Plain text passwords
Broken Access Control
Cryptographic Failures
Identification & Authentication Failures

### Scope of Testing
https://www.hackthissite.org/missions/basic/
Levels 1 - 11

### Recommendations
1. Encrypt all sensitive data at rest.
2. Store passwords using strong adaptive and salted hashing functions with a work factor (delay factor), such as Argon2, scrypt, bcrypt or PBKDF2.
3. Don’t store passwords in the source code.
4. Except for public resources, deny access by default.
5. Disable web server directory listing and ensure file metadata (e.g., .git) and backup files are not present within web roots.
6. Audit all source code to verify no sensitive information is published in it.
7. Set up access control to ensure in cases of no stored passwords that no access will be given.
8. Remove publicly available password resets.
9. Don’t reveal encryption methods. Ensure that cryptographic randomness is used where appropriate, and that it has not been seeded in a predictable way or with low entropy.
10. Don’t store passwords or access controls in cookies accessible to the user.
11. Use positive server-side input validation. 
12. Implement input sanitation.
13. Implement secure design.
14. Implement MFA

### Summary of Found Vulnerabilities
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/fd7241b2-3b75-4559-bf6a-5e6b100a344d" width = 600>
</div>

### Found Vulnerability 1: HTML Source Code
On level one, the HTML Source Code reveals the password in the console.

#### Remediation: 
Passwords should never be stored in plaintext. They shouldn’t be stored in the source code. This password should be deleted from the source code, then it needs to be changed, and an audit of all the source code for the website should be done to ensure no other passwords are easily available. 

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/161d26ad-196a-40d1-9593-30a525565e13" width = 600>
</div>
<br>
<br>

### Found Vulnerability 2: No password required
On the login page for level 2, no password is required due to not uploading the correct password to compare the entry to. 

#### Remediation: 
Upload the password. Set up the access control so that if there is no stored password for anything in the future, the default setting would be to not allow entry.

<br><br>

### Found Vulnerability 3: Password File Accessible to Public
In the source code, the file name for the password can be seen: “password.php”.

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/447ed0ba-35a2-4d91-bc39-926237acbcd9" width = 400>
</div>
<br>
When searching for this file on the web server by adding this file to the end of the url, the password was returned.
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/c767b865-9c6e-4615-b699-ddeb3e3f28fe" width = 400>
</div>

#### Remediation: 
Set up better access controls for all of the files on the web server. Audit other files with sensitive information to ensure proper access control.


<br><br>

### Found Vulnerability 4: Editable Email Address Recovery in Source Code
On levels 4 and 5, the website allows the user to send the password to a pre-designated email address. 

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/2d3ae3b4-52e7-427a-99e0-d3941f502cc7" width = 500>
</div>
<br>
However, in the source code, this email address can be altered to any email address associated with an account on the website. By editing the source code to one’s own email address, any user with an account can receive the password.
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/dc982687-ded7-4223-a415-e0cd44263c68" width = 500>
</div>
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/ef6e00dc-54ca-451b-a3f2-b39def1856da" width = 200>
</div>

#### Remediation: 
Remove the publicly available password reset. Remove the ability to change the email in the source code.

<br><br>

### Found Vulnerability 5: Can Reverse Engineer Encryption Method
On level 6, there is an encrypter and a note about what the encrypted password is. If one can figure out the method of encryption, they could then decrypt the password given.

I used several test passwords to reverse engineer the encryption method. I started with single letters: “a”, “b”, “c” and noticed all of them returned the same values. I then made the passwords longer, such as “abc” and “abcd”. I noticed there was a pattern to how their values were changing. I then experimented with numbers and symbols to see if they were handled similarly. 

#### Test password and its encryption
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/9a69623d-0c6a-4c2a-80e9-ca37ac13d52f" width = 600>
</div>
<br>
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/c79935c1-6d10-47b8-8a6e-9c4ef1aa8f6a" width = 250>
</div>
<br>

#### Pattern: 
1st character -> same 
2nd character -> shift 1 to the right of the [ASCII table]([url](https://www.asciitable.com/)) 
3rd character -> shift 2 
4th character -> shift 3 

#### Conclusion of Pattern:
Given that n = character placement and placement starts at 0, the encrypted character = original_character + n

#### Decrypted Password:
Encrypted Password is: 05e;e:lj 
Pattern to Decrypt: shift positions --> same, -1, -2, -3, -4, -5, -6, -7 
Decrypted Password is: 04c8a5fc

#### Remediation:
Remove the ability to encrypt any password on the website. Do not reveal the encrypted password. Choose stronger encryption methods.

<br><br>

### Found Vulnerability 6: Injection
On level 7, the input field is vulnerable to linux injection attacks to find the password for level 7 and 8. 


<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/709d438e-4bd9-43ce-9c6f-6b47cc01a591" width = 600>
</div>
<br>
By injecting “2024;ls” I was able to get the name of the password file.
<br>
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/030b4ee3-78be-4c1b-931b-9dfbab0cef47" width = 250>
</div>
<br>
I was then able to navigate to this file via editing the url and retrieve the password.
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/c98eefe7-88d4-4fb7-b5d0-15518383d226" width = 400>
</div>

#### Remediation:
Use data sanitization and server side validation for input fields. 

<br><br>

### Found Vulnerability 7: Lack of Server Side Validation
On level 9, the input field is vulnerable to injection attacks. I first tested to see what it would do with odd symbols and it treated all symbols as if they were regular letters or numbers. 


<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/21cae8e4-c39c-4032-829a-839d83e36846" width = 300>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/12dc5e5d-84ba-45d3-9628-c493919f85e4" width = 400>
</div>

<br>
I then injected the following command, which revealed the password file name.

Injected: ```<!--#exec cmd="ls ../" -->```

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/5122f270-9eec-4067-80fd-224e25b87de6" width = 400>
</div>

<br>
I navigated to the password file and retrieved the password.

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/7071dd60-bbf5-4306-857b-ff185bec0566" width = 400>
</div>

#### Remediation: 
Use server side validation and data sanitization. Put access controls in place for files with sensitive information.


<br><br>

### Found Vulnerability 8: Editable Cookies - Allow Access, Password Info
On level 10, the user can navigate to the console and find the password stored in the cookies. 

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/ed31b70d-0f32-499c-a7ec-f82c7e7e6771" width = 400>
</div>

They can also change their access to the webpage via another cookie.

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/e1b4c437-c9c4-4d64-9f6d-f2980409cf33" width = 400>

#### Remediation:
Don’t store the password in plain text in a cookie. Use hashing and salting techniques. Do not allow for an access change via a cookie.

### Found Vulnerability 9: Public Access to Files

On level 11, any user could figure out the name of the file with the password and open that file on the web browser.

#### Remediation:
Limit access to files with sensitive information.
</div>
