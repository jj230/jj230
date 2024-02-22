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
The security vulnerabilites found in this section of the website allow unauthorized access to all areas in the /basic/ section. These vulnerabilites can be easily remediated. 

### Scope of Testing
https://www.hackthissite.org/missions/basic/
Levels 1 - 11

### Found Vulnerability 1: HTML Source Code
The HTML Source Code reveals the password in the console.

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/161d26ad-196a-40d1-9593-30a525565e13" width = 600>
</div>
<br>
<br>

### Found Vulnerability 2: No password required
On the login page for level 2, no password is required due to not uploading the correct password to compare the entry to.

<br><br>

### Found Vulnerability 3: Password File Accessible to Public
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/447ed0ba-35a2-4d91-bc39-926237acbcd9" width = 400>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/c767b865-9c6e-4615-b699-ddeb3e3f28fe" width = 400>
</div>

<br><br>

### Found Vulnerability 4: Editable Email Address Recovery in Source Code

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/2d3ae3b4-52e7-427a-99e0-d3941f502cc7" width = 500>
</div>
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/dc982687-ded7-4223-a415-e0cd44263c68" width = 500>
</div>
<br>
<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/ef6e00dc-54ca-451b-a3f2-b39def1856da" width = 200>
</div>

<br><br>

### Found Vulnerability 5: Can Reverse Engineer Encryption Method
Test password:

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/9a69623d-0c6a-4c2a-80e9-ca37ac13d52f" width = 400>
</div>

Encrypted test password:

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/c79935c1-6d10-47b8-8a6e-9c4ef1aa8f6a" width = 400>
</div>

Pattern:
1st character -> same
2nd character -> shift 1 to the right of the [ASCII table]([url](https://www.asciitable.com/))
3rd character -> shift 2
4th character -> shift 3
encrypted character = character + n; given that n = character placement and placement starts at 0

Conclusion:
Encrypted Password is: 05e;e:lj
Pattern to Decrypt: shift positions --> same, -1, -2, -3, -4, -5, -6, -7
Decrypted Password is: 04c8a5fc

<br><br>

### Found Vulnerability 6: UNIX injection

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/709d438e-4bd9-43ce-9c6f-6b47cc01a591" width = 400>
</div>

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/030b4ee3-78be-4c1b-931b-9dfbab0cef47" width = 400>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/c98eefe7-88d4-4fb7-b5d0-15518383d226" width = 400>
</div>

<br><br>

### Found Vulnerability 7: Lack of Server Side Validation

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/21cae8e4-c39c-4032-829a-839d83e36846" width = 400>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/12dc5e5d-84ba-45d3-9628-c493919f85e4" width = 400>
</div>

Injected: <!--#exec cmd="ls ../" -->

<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/5122f270-9eec-4067-80fd-224e25b87de6" width = 400>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/7071dd60-bbf5-4306-857b-ff185bec0566" width = 400>
</div>

<br><br>

### Found Vulnerability 8: Editable Cookies - Allow Access, Password Info
<div align="left" data-full-width="false">
<img src="https://github.com/jj230/jj230/assets/93885534/ed31b70d-0f32-499c-a7ec-f82c7e7e6771" width = 400>
</div>

<div align="left" data-full-width="false">  
<img src="https://github.com/jj230/jj230/assets/93885534/e1b4c437-c9c4-4d64-9f6d-f2980409cf33" width = 400>
</div>
