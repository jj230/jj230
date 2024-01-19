# SHA256 Password Hash Cracking

I created this script during TCM's Python 101 for Hackers course.

On a Kali Linux VM through UTM, I created a python script for cracking a SHA256 hashed password using Sublime. I then tested it using a password I knew was in my chosen password file until it was successful.

## Code

This is the final script.

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/5afd8d25-1a26-4d18-81f3-b15a0df9e85d)" width = "850">

</div>

## PROCESS

### Password File
I chose to use the rockyou.txt file that was already installed on my kali linux vm. I used gunzip to unzip it and verified the file looked as it should.

<div align="left">
  
<img src="https://github.com/jj230/jj230/assets/93885534/9f4a2a7d-559a-4a16-be2d-a13e15875c0c" width = "600">

</div>


<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/815b6227-c6f8-47fc-94c3-8d672c48194a" width = "350">

</div>


<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/633013c8-b198-4d11-8320-0ff3c16d04ac" width = "600">

</div>

### Finding Password for Testing Script

In order to test the script, I needed to test it against a password in the list. I didn't want to choose the first password, because I wanted a couple of seconds to see the script run. I also didn't want to choose the last password because it would take a while. So, I used sed -n and p to print a password that was in the list that was close to the beginning but not too close.

<div align="left">

<img src= "https://github.com/jj230/jj230/assets/93885534/6dab40fa-8ee4-4528-9e67-23ecb4f4c03a" width = "400">

</div>

### Debugging

#### Bug #1 - Mistyped "progress"

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/5e67632b-ca77-400a-bbf4-735043a85766" width = "400">

</div>

#### Bug #2 - Didn't properly identify path to rockyou.txt

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/134b4ccd-63ec-403a-b3a2-3adacf457b53)" width = "400">

</div>

#### Bug #3 - Didn't save password in encoded format

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/24846182-f140-4fff-93af-9dae9fd860c8)" width = "400">

</div>

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/3ff8a996-da06-4491-8b9c-4d349616abcb)" width = "500">

</div>

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/b58d8f5e-3819-4427-bc49-dfcd628aed8e)" width = "500">

</div>


#### Bug #4 - Needed to save in hex format rather than in binary

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/b60d0651-b169-4d0b-a9f4-050320ddaab9)" width = "350">

</div>

### Success!

<img src="https://github.com/jj230/jj230/assets/93885534/e674c58e-10bb-4434-9504-56f147d8d9a5)" width = "700">



