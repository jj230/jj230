# Linux PrivEsc

### Tools/Skills 

Linux CLI, assigned privileges, command injection, privilege escalation

---

## SYNOPSIS

From inside of a user's (non-root/admin) account, run a binary that's stored in root.

By identifying a command that allowed for unintended privilege escalation (simplecopy), I was able to copy the root directory, including the binary into my account. This allowed me to see the name of what I needed to run. From there, I was able to use a command injection to escalate my privileges to root long enough to run the binary.&#x20;

## Clue

<figure><img src="https://lh7-us.googleusercontent.com/aQi8VhBhAeOJcaMNieW2M3qnK702c2xjuWld-JmLeUBauwgLpV6IULd_qqfHnsb3FCWduTp51FUemfvcMgm8aMdw8qPD9PMYp7Kx2XW4Rp3sFoZ7Wew9HSznlpINqQ_jGh-3HKe6vkAsR9P2kvmigkY" alt=""><figcaption></figcaption></figure>

## SOLUTION

1. Identify the command that allows for unintended privilege escalation: <mark style="background-color:red;">`simplecopy`</mark>
2. Copy the root directory into the elf directory → observe the name of the file in the root directory: <mark style="background-color:red;">`“runmetoanswer”`</mark>

<figure><img src="https://lh7-us.googleusercontent.com/gH3VXhMfznuXw7LnlHCWAe7Lb3V81IQpY4blT5MNFUuS2ZELO7gkk_95uRWipmsdtMSdaDGxJEUUWc61MBFHG3LL4x_jryJU7rPndq8OGKifQnDCLb-ev93h4sWXkat9JWpX8FROWPteIedf8phXbsA" alt=""><figcaption></figcaption></figure>

3. Remember the hint: “escalate privileges inside this terminal and then run the binary in /root”
   * <mark style="background-color:red;">`simplecopy`</mark> → escalates privileges
   * <mark style="background-color:red;">`/home/elf/runmetoanswer`</mark> → would run the binary if I had escalated privileges.
   * Combine: <mark style="background-color:red;">`simplecopy /root/* "/home/elf; /home/elf/runmetoanswer"`</mark>
   * Answer: “santa”

## PROCESS

1. A lot of trial and error
2. A lot of the hints in the discord channel that others had provided
3. I used ChatGPT anytime I thought it might help (and even some moments I didn’t think it would, but hoped it might)
4. My first moment of hope: When I managed to successfully copy the root directory into my directory. This allowed me to see the name of what I wanted to execute, but I still couldn’t execute it.&#x20;
5. Discord Hints
   1. Simple Copy
   2. Should be one, simple command
   3. Command Injection
      * Consider different ways to combine commands
   4. [Link for how-to do a command injection](https://owasp.org/www-community/attacks/Command\_Injection): Ultimately this led to me figuring out the answer
   5. Extra trial and error for:using the quotation marks, where to put the quotation marks, the semicolon, and the space after the semicolon.

***

## [ChatGPT Prompt/Answer](https://chat.openai.com/share/2494b672-940b-4b46-8d0e-1df897f0f679)

#### Example Prompts:

* Would any of these contain information about ways to perform a privilege escalation? .   .dockerenv  boot  etc   lib    lib64   media  opt   root  sbin  sys  usr ..  bin         dev   home  lib32  libx32  mnt    proc  run   srv   tmp  var
* How do I list with information about access?
* What are command separators?

\
