# Elf Hunt

### Tools/Skills 

Browser's Developer Tools, HTML, JavaScript, Runtime Modifications, Burp Suite, JSON Tokens

---

## SYNOPSIS

In a computer game, I needed to stop 75 elves by clicking on them. These elves were fast and kept changing directions.&#x20;

A provided hint suggested that I look at modifying the JSON token.

The way I solved this was with runtime modifications, altering variables in the console with Chrome's Developer Tools.&#x20;

I also tried to solve this in two other ways:&#x20;

1. I tried to solve it with Burp Suite to modify the response. This way I believe would have worked if I was paying for Burp Suite, but I was unable to verify.&#x20;
2. I tried to solve this by editing the response within the Developer Tools. I haven't yet figured out how to make this work, but may head back to it at some point.

## SOLUTION & PROCESS

### 1ST WAY:

1. Go to console
2. Inspecting the variables
3. Slow down the elves by changing their x and y velocity
4. Get to the 75 points

\*Note: I knew I hadn’t done anything with the JSON tokens, though, and figured there must be a second way.

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/YPbrRrRiwjNiUtF4KasE3-a80V7M9z4WZufW0l6BkYpqZuPmTgBSAReTveNF-L29QebXJSzZMLpVFp1ociHqgfVzOMvfFdpxF0SPZBhGNgev0ktqe9-A4n8jVejWUuyQ7aeSyIjVFdnDGCr-ZgcLZo8" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/x5wmB36s113jdcTyZ0PPNKG0SEfiWIXhloN6NG8t7aUAq68XalRiuZyTxVCGR9aIeKVW_yUjwtQH72WjFS-AnrzGhDNSVl-m1PMnGwLEKxrO8nJ6QiZnCMVn9nJLaJ7xuRKCfvy-OII2ffYOTDPRsB8" alt="" width="375"><figcaption></figcaption></figure>

</div>

### 2ND WAY:

1. Researched on the discord channel
2. Found a youtube video
3. Used ChatGPT to find out how to use Burp Suite to modify responses
4.  I got up to the point where I would’ve been able to edit the response and send it, but couldn’t do so without a paid version of Burp Suite.

    <div align="left">

    <figure><img src="https://lh7-us.googleusercontent.com/DJXfR4oBid5jsb0XCzP_6mYdobkabPiQ027UvIqB21k1HJIuUPB2s9M-Z0JM_gVtZ8YCPB1gKvzWPSsYa4Lmlp8WfmgoOKVShSVh-aCbk2Wcsx-5yQUqsQmdW34_3N1QVsYpvkxSKFp7710a0dKyKBY" alt="" width="563"><figcaption></figcaption></figure>

    </div>

### 3RD WAY:

1. Go to developer tools on chrome
2. Go to response and set it up so it can be edited
3. Save & apply changes

\* I haven’t yet figured out this last step. But, having already found other ways to accomplish this task, I paused and decided to retry it some other time with a fresh mind.

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/u-ZldhrSCXrsxzc0felX1RyteyY-vCI4psJJE65aqO6xfkASDV7oibw6FbUJ0zw9f43vaYLYUVZd9vFEjLZpGnN3LZunnCVeW4QrPbferL8kp25CaH0-jNeU350svHNJNL2WfB3oiAl0drJRNYQlaqE" alt="" width="563"><figcaption></figcaption></figure>

</div>

***

## [ChatGPT Prompts/Answers](https://chat.openai.com/share/3ab03d9a-a3ae-443e-97b5-75855ee6be72)

#### Example Prompts:

* How do I edit a response in Burp Suite?
* Is there a way to edit responses in the free version? or without Burp Suite?

## [Bard](https://g.co/bard/share/b3f50244573f)

#### Example Prompts:

* Is there a way to edit a response in chrome using developer tools?
* I'm trying to follow method 1. For some reason, when I choose "override content" nothing is happening.
