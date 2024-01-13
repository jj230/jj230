---
description: 'Tools/Skills: Azure CLI, Azure Cloud Environment'
---

# Azure 101

## SYNOPSIS

The goal is to learn about the North Pole's cloud environment, including VMs and other resources with the use of Azure.

Through the challenge, I found account info, resource groups, functionapps within a resource group, and details of virtual machines. I also invoked a run-command to reveal a file in a vm.&#x20;

## SOLUTION

1.  Go to azure help menu

    <mark style="background-color:red;">`az help | less (help menu)`</mark>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/OAOt_nE7zJhlO7pZ_47Y9xL2fHpz1v4RBgSh1e5ueBceKqomF2TjnGaCDZ4Puui33KmbLthMMP9NtzEYrTy6c6iwTf55YffCNr5U1jBJX-n8QDbKKc5PKdRS7CF9DleeQlKJjKy6VcriXL9nJcaxBhM" alt="" width="563"><figcaption></figcaption></figure>

</div>

2.  Show Account Info

    <mark style="background-color:red;">`az account show | less`</mark>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/P4hvhLAiK9YztNNI6Q49S4AMRQ3xiqdB8ogEdsBNQ_GKPX6QSKGIj6zv--9ukZZAu2OR020uI077Yci3wbvtbcXfEelVnEOkkHD7jQz0ciDV0Q3ruIOJrfwijKA66g8Cyf7aI29HxXt4hYcUocenhcg" alt="" width="375"><figcaption></figcaption></figure>

</div>

3.  List Resource Groups

    [<mark style="background-color:red;">`az group list | less`</mark>](https://learn.microsoft.com/en-us/cli/azure/group?view=azure-cli-latest)

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/pSSD6wnD9w0Wm4KJN8w5rVkaJiD3093JQ5txvkVsI121fb4G6iVyS8sU1X7WLcfEKwNRbM8vRRyzu8kJupqhV6THwajGgahD3DwO4MnW7dDQTBBgr2zwfJzRgf6m7zLIP01V8rc87J2JEFGHCrIc3-4" alt="" width="563"><figcaption></figcaption></figure>

</div>

4.  List all functionapps in Resource Group “northpole-rg1”

    [<mark style="background-color:red;">`az functionapp list –resource-group northpole-rg1 | less`</mark>](https://learn.microsoft.com/en-us/cli/azure/functionapp?view=azure-cli-latest#az-functionapp-list)

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/N2eOmMQt9tiYAHUqUWenzYfadcLo8a1Ynk16-prp_lt0l5mFH7xM3a7eIEbQuCNXlQ4VKLmexIrrCrDIDNhm_N226u5GViFYTH3eIUZFJh8LHG5yLW_ysSSxkqWGiC9kpV8vnWH8lCIfHAfqhqF2wJg" alt="" width="563"><figcaption></figcaption></figure>

</div>

5.  List details of virtual machines in the Resource Group “northpole-rg2”

    [<mark style="background-color:red;">`az vm list -g northpole-rg2 | less`</mark>](https://learn.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest)

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/BiPLE1Rs82lYt3efEPMT0CFQo8rpB1YWuY3PfBamMWMNzi2LfZIAAin1n4R7fkuuRlfz3rJGivfJz9bBp8crzwySe0wMG1YpQPhzWFK5LRmP5PgSOk4Rnbc8AwZmZTjtOYZUoEGcZVlQy0WDqwl11tc" alt="" width="563"><figcaption></figcaption></figure>

</div>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/35mFY8D8jLaQ4BX94x9mBdXuQL2qqQlar72eEjk4bM5D4dJ5hDohxd0yWHufJbTO3X4gvQ5w4Zv722MUD3WcT4GjefUOTPCR5Io-yegeR7SZpHcVaQSH3S5XmpWzxMrSuoQdeNqn-SCG6UgbUkq6IkI" alt="" width="375"><figcaption></figcaption></figure>

</div>

6.  Invoke a run-command against vm and RunShellScript to get a directory listing to reveal a file on the Azure VM

    <mark style="background-color:red;">`az vm run-command invoke --resource-group northpole-rg2 --name NP-VM1 --command-id RunShellScript --scripts "ls -l" --output json`</mark>

<div align="left">

<figure><img src="https://lh7-us.googleusercontent.com/zjTg7gvHbNDXjIwMt6N-mWiFFPdZmy5fGCQ--DJHKMDWoHT9o7XfRmR1KjT__64zziM8CjKuJyP7r8CKV6KFaZlgDUDYTY0CmYAi8UA9pG_cjPwsyEeuQ9socEdwHPD7CN3m4fMDMP-bWXAIW0vm7x0" alt="" width="563"><figcaption></figcaption></figure>

</div>

***

## [ChatGPT Prompt/Answer](https://chat.openai.com/share/2947212e-660d-4288-8380-00e886a35f1f)

#### Prompts:

* How do I: Find a way to invoke a run-command against the only Virtual Machine (VM) so you can RunShellScript and get a directory listing to reveal a file on the Azure VM?
* What do I need to change about this command to have it list the directory? az vm run-command invoke -g northpole-rg2 -n NP-VM1 --command-id RunShellScript\
