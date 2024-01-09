---
description: >-
  Tools/Skills: Linux CLI: ls, pwd, cat, rm, cd, chmod, grep, find, history, ps
  aux, netstat, curl, kill
---

# Linux 101

## SYNOPSIS

Find all of the trolls in the system. Specific instructions were given to find each troll.

In the process of finding the trolls, I performed the following functions:&#x20;

* List files/directories (including hidden ones), open files, remove files, identify location in system, display command history, change directory, search for a word within the files, run a binary, change permissions, copy a file, rename a file, write to a file, make a symbolic link, use find to search by name/user/file size, list running processes, display listening ports, use 'curl' to interact with server, stop a process using 'kill'
* I used the following base commands: <mark style="background-color:red;">ls, pwd, cat, rm, cd, chmod, grep, find, history, ps aux, netstat, curl, kill</mark>

[ChatGPT Prompts/Answers](https://chat.openai.com/share/006a52f6-e4fe-4e22-a75c-b8f2a9e0f9ee)

Example Prompts:

* How do I find environment variables?
* How do I make a symbolic link?
* What is a symbolic link?

## SOLUTION

The following are the commands and results of each step of the linux 101 challenge.

<figure><img src="https://lh7-us.googleusercontent.com/eGKwaEre3T8rxQFBnqlxoEbGBJxrGXpTnbT5K_Ps0pxmR38ItzwjAHdRqJOlFMM98KhgZKXaQi583QWtzwctw59rkKMG1USnrMqqZC6XKBB2ttIuOuc6afoZ9Kzw7_No693YN7wqqUXsiOvNorVeQmM" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/rx4NslQFhseB8qmcR0M0TtvSfZCANGGy2mWAZ3K5bMCt5KUnetC3LS6FNvCXLtPgmC0Yn6rHY_jgaWtCb4vlVQXxDelrNllhfR6L6WeDzC8n4aV9aYzWwLxnQeQVbsgkpvWWB2lOHasVP6aMZ28sqo4" alt=""><figcaption></figcaption></figure>

find “troll” /opt/troll\_den

\*Note: The below code took a few attempts, because I took the instructions more literally than intended. It said to find a specific file size between two amounts that was created by trolls. I eventually decided to try to run the command without specifying the user or creator. It worked.

<figure><img src="https://lh7-us.googleusercontent.com/6ZJ1pK8qOnkLnSrbLcS23ez9Ltvo-oqKqZuSC6_SyqJoTV5uPBdHvK9YGB5iSycdI4jU08IgxgIvLprESs-37c4DxVVUhvQUoQ2_ewgjqovuwSeIZExIqRXF2Cs_Ifl-u0ixpK0IFlmBfjVFq-uX3TU" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/OlfXeAGNlw_akr-ftN5zjO_GjmKvUx3PMMu6TBVbRF_dqSdlWAklN8aSAJuZiCRzctH_pQM75fKzS6MWI7jtflXrMiN2GBD0XU08VXla7dq_pfrlDIkUdxNQHGtM1ENk-XoN9OgPN0JR-riPgAltQVM" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/LxnsNfaGFK0g55aOfLr2ZTeXdvNv9K4XrAx08JwzEaW7-tMP2o2a_gNys8mBHjv3zlyhLq31eTBKgA2azIzIpO9CMeILaAMG2Py_EQcitA2lNMbzK1p6BhkA05fLR0MF_t8okIl6ki42PBMkLmQQW74" alt=""><figcaption></figcaption></figure>

Once I finished this, I had to re-do it. I had been logged out. I took advantage of re-doing it to cement the commands further into my memory. I also did some research when it came to the find command. I remembered last time, the command I used gave me too many results. So I received a hint from the game and asked bard a question about the asterisks that were used. Together, I understood better how to get the best results for that search.

[ChatGPT Prompts/Answers](https://chat.openai.com/share/f179a63d-feaa-479f-b569-bcd322ff589b)

Prompts:

* What's the point of the asterisks? find /opt/troll\_den/ -iname "\*troll\*"
* Can you specify who a file is created by when using the find command?
