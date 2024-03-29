# Phish Detection Agency

### Tools/Skills 

Identifying Phishing Emails, DMARC, DKIM-Signature

---

## SYNOPSIS

A phishing identifier isn't working perfectly, so I needed to go in and verify that phishing emails were correctly marked and that non-phishing emails were not mis-labeled.

By reviewing the return-paths, received domains, problems with the DKIM-Signature and when the DMARC failed, I correctly identified all emails as either phishing or not.&#x20;

Recommendation: A program should be able to be made or updated to correctly capture the phishing emails I identified. If the program automatically labeled the following cases as phishing emails, it would have had 100% success (based on this example - further testing would be required): 1. A different return-path 2. A different received domain 3. Problems with the DKIM-Signature 4. Failing the DMARC.

## SOLUTION & PROCESS

1. Reviewed all emails
   * [x] A different return-path or received domain → phishing
   * [x] Problems with the DKIM-Signature → phishing
   * [x] Failed the DMARC → phishing&#x20;
2. Other techniques
   * I set up  my search bar (command + f) to always looking for the domain “geeseislands”&#x20;
     * It didn’t end up revealing any phishing attempts, but I did because this would be an easy typosquat to miss
   * I was prepared to also look for unusual dates and times, as well as content that didn’t seem to match the domain, but I didn’t end up needing to.

\*I used a couple ChatGPT prompts to help ensure I was on the right track.

***

## [ChatGPT Prompts/Answers](https://chat.openai.com/share/88f5e0a1-c230-4a90-b4ff-68d9a07af6cb)

#### Example Prompt:

* What clues in this email could I look to decide if it's a phishing email or safe?

> Email Details
>
> From: laura.green@geeseislands.com
>
> Reply-to: admin.security@geeseislands.com
>
> Date: 2023-07-20 09:15:00
>
> Subject: Security Protocol Briefing
>
> Email Headers
>
> Return-Path: \<laura.green@unauthorized.com>
>
> Received: from unauthorized.com
>
> DKIM-Signature: v=1; a=rsa-sha256; d=unauthorized.com; s=default; b=HJgZP0lGJb8xK3t18YsOUpZ+YvgcCj2h3ZdCQF/TN0XQlWgZt4Ll3cEjy1O4Ed9BwFkN8XfOaKJbnN+lCzA8DyQ9PDPkT9PeZw2+JhQK1RmZdJlfg8aIlXvB2Jy2b2RQlKcY0a5+j/48edL9XkF2R8jTtKgZd9JbOOyD4EHD6uLX5;
>
> DMARC: Pass

\
\
