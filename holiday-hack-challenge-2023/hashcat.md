# Hashcat

### Tools/Skills 

CLI, Hashcat, Hash Types

---

## SYNOPSIS

A file with a hashed password needs to be decoded by first identifying the type of hash and, then, using hashcat.&#x20;

I identified the hash by comparing the hash in the file to a list of different hashes and what they look like. Once identified, I selected the necessary options to identify the type of hash (-m 18200) and the type of attack (-a 0), and joined those options with a list options I needed to include to slow down the command (-w 1 -u 1 --kernel-accel 1 --kernel-loops 1 --force).

<figure><img src="https://lh7-us.googleusercontent.com/d8Srh43agpHPGS_isVRMhT6oE62C1agdvJ3Cu3LX0-j0Y2kRoQU57TAbN_6HtBMyc5p1lr_yeOrjzQlNoxEGQxgFOxX1f_YzqQXFhq7oM_Jc7GEWHE8LcQn0zwxqbBRjIc0thjs-qw9LjMyGtPV71aE" alt=""><figcaption></figcaption></figure>

## SOLUTION & PROCESS

1. Hash Type
   1. Compare the hash file in hash.txt (cat hash.txt) to hashes in the [link provided](https://hashcat.net/wiki/doku.php?id=example\_hashes).
      1. In hash.txt there was a unique beginning, including an “@” symbol.
      2. Based on the “@”, I narrowed the type down to Kerberos 5 etype 23 AS-REP
      3. I missed that it said AS-REP, so I had to try [a few of the options ](https://hashcat.net/wiki/doku.php?id=hashcat)out before I figured out the exact type and the password.&#x20;
2.  Input correct command

    <mark style="background-color:red;">`hashcat -w 1 -u 1 --kernel-accel 1 --kernel-loops 1 --force -m 18200 -a 0 hash.txt password_list.txt`</mark>

    \*Many of these options were provided in instructions to slow down the command

    \*Identified attack type (dictionary, -a 0)

    \*Identified hash type (-m 18200), hash file, password file
3. Identify cracked password
   *   After the password was cracked, it took me a few more minutes to figure out the answer was provided at the end of the hash in the results rather than after “Candidates #1”



       <figure><img src="https://lh7-us.googleusercontent.com/juuI71iyuuVLLi6rmforZO1q2AZbhVObHHcFTHvQ7KG2Tc2NysjX4jNZFnayP19YOWOOdja_ZdPmH5s5y_1ZCVNXyqP0j8AYj2m8xNHE6w1ZuEZOmx57pwGuRFeZo0LiT_4qdz-MRJlJwcPQLULdJW4" alt=""><figcaption></figcaption></figure>

       PASSWORD: IluvC4ndyC4nes!
4. Input answer to /bin/runtoanswer

## SUMMARY

<mark style="background-color:green;">**Hash Type:**</mark> Kerberos 5 AS-REP etype 23 AS-REP

<mark style="background-color:green;">**Command:**</mark> `hashcat -w 1 -u 1 --kernel-accel 1 --kernel-loops 1 --force -m 18200 -a 0 hash.txt password_list.txt`

<mark style="background-color:green;">**Password:**</mark> IluvC4ndyC4nes!

***

## [ChatGPT Prompts/Answers](https://chat.openai.com/share/3d94d83c-6950-4999-88c9-143a5e45fbb5)

### Example Prompts:

* What does this command do? \`-w 1 -u 1 --kernel-accel 1 --kernel-loops 1\`
* How do I use hashcat?
* Can I use hashcat without knowing the hash type?

\
