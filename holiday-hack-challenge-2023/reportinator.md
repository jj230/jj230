---
description: >-
  Tools/Skills: Burpsuite - proxy, intercept, logger, intruder, cluster bomb,
  payloads, HTTP traffic
---

# Reportinator

## SYNOPSIS

A vulnerability report of 9 vulnerabilities was created with the help of AI. Some of the vulnerabilities are hallucinations. My job was to figure out which ones.&#x20;

Initially, I approached the task by trying to understand the vulnerabilities and identify which were the false positives/hallucinations. After two days of off-and-on working on this, I realized that even with the help of AI, that identifying the signs of a hallucination would take a lot more time.&#x20;

With the help of some clues I read on discord, I switched tactics. I used burpsuite to intercept the HTTP traffic that was created when I gave a possible answer to the question. I, then, analyzed the logs, figured out what part of code referenced my answers, and created a clusterbomb attack to try all possible answers. In less than a half hour, the 200 code popped up, showing that I had found the hallucinations.

## SOLUTION

1. Download Burp Suite
2. Proxy -> Intercept On (use Chromium)
3. Analyze Logger → Identify the inputs as the values/answers that I wanted to experiment with

<figure><img src="https://lh7-us.googleusercontent.com/17avSVe9qRBOFV6gjBGUj0N71j45sDciS961hBGHSk8eez4ETJI8HLMBSRVpvA9ij42gdGRKQZNfBpNUgPefEhsvr443LILxpfqfmOD02Kli6Stw2iz__hQn0t8BOSb8CtkTWxbe-fNqorCK4v_jcuQ" alt=""><figcaption></figcaption></figure>

4. Intruder → Cluster Bomb → Added Payloads → Adjusted Payloads to Integer between 0 and 1 → Start Attack

<figure><img src="https://lh7-us.googleusercontent.com/OVsPplp4rfAzioGAnuIYV-5evtDzdFByj7Z-_2qNhAvYlt-tV4anX31irPXMWL6obBrKYw2-lXQr2-4h8iiE8dpN7aqazF7nsIitiUgT0G4FK4QuCwZQQC3v6xi_6GiMVgVcUrojO3Ynov0J0-pPpnI" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/e5Dei28G-8S5GuPDpq-zzKzoszmkUFSLGahJ6dYm3Dzw6wshg8EcsEDWeufSyDWAYDUoDkPVl1g_wGRYnQyT9eiKu-JhMTst6cj4ud_XG0v1oXOtnISORKAdh0AacRP-k9lZsQ3wkHVahgUOsJ-YwZo" alt=""><figcaption></figcaption></figure>

5. Waited until a 200 Code showed up → Success

<figure><img src="https://lh7-us.googleusercontent.com/X_fuUc7tSHR1OhbHJuICIYo345kQxTfCCyO_RILHoy43fPTbxkOs9Ul8UQpYglQUkQjCKxYHDk9nsH4KQLPR90JbmxhdgJf_Pj7_R_kdfm-klJ7rc-CmqoxK9v_UCd5ndAKngsFMln2h24NxIfC_e9M" alt=""><figcaption></figcaption></figure>

6. Based on the input values of 1, I identified Questions 3, 6 and 9 as the hallucinations.

## PROCESS

1. Can I figure it out on my own? → No
   * I attempted going through the first five or six potential vulnerabilities with a fine tooth comb. → I was no closer to finding the answers.&#x20;
2. **Can ChatGPT or Bard decide on the correct answers?** → Nope.&#x20;
   *   I tried both of these to see if they could spot something I couldn’t, but they couldn’t. They even disagreed with each other.

       ChatGPT Attempts:

       * [1st Attempt](https://chat.openai.com/share/cb602056-408a-49ba-9150-f90e25d67ce2)
       * [2nd Attempt](https://chat.openai.com/share/ebb1a3bd-27b4-4703-861f-40393bd08f35)
       * [3rd Attempt](https://chat.openai.com/share/af1e71bd-8359-41dc-b00f-13022da2e977)
       * [4th Attempt](https://chat.openai.com/share/32124fc0-e4ec-4264-87af-0d5a676fe7da)
       * [5th Attempt](https://chat.openai.com/share/de238ab2-3ff1-48b2-9b9a-b73f99cc94e1)
       * [6th Attempt](https://chat.openai.com/share/7d423028-eff5-41c0-a287-6a380f87825b)
       * [7th Attempt](https://chat.openai.com/share/76e8a203-5422-4430-9708-3195e835fad7)
       * [8th Attempt](https://chat.openai.com/share/f935baed-852f-48ef-bfe1-5c6ae0dfc2ae)
       * [9th Attempt](https://chat.openai.com/share/c886c98f-7ab6-4fd6-831e-9eb337ebc7c4)

       Bard Attempt:

       * [Attempt](https://g.co/bard/share/00c98e8470cd)
3. Can Discord help?&#x20;
   * Burp Suite? I’d heard of it, but hadn’t yet used it.&#x20;
   * Downloaded Burp Suite.
   * Cluster Bomb?&#x20;
   *   [Bard Prompts/Answers](https://g.co/bard/share/4060d294e46f)

       Prompt:&#x20;

       how to use cluster bomb in burp suite
4. Watched a video on how to use the “cluster bomb” method for a username/password list.
5. Analyzed how my answers were showing up in the code (as 0s and 1s) and adjusted the cluster bomb method for numbers instead of a list.
6. What’s a way I can test out every possible solution without doing the work myself? → Yes
7. Burp Suite Learning & Success
