# Updating File - Allowed IP Addresses

### Project description

I created this algorithm during Google's Cybersecurity Certificate Program.

I used python to create an automated function that will update a file with the correct allowed IP addresses, removing any that are no longer allowed. A screenshot of the full code, all-together is below. The individual steps are labeled within the code as well as below the screenshot.

### From Function to Script

While this code itself is written as a function more than a script, it could be written as a script as well. To change it to a script, I'd update it to include the paths to the import\_file and remove\_list. For example, I could write this as a script so that anytime someone marks an IP address as needing to be removed, this script automatically runs and removes it from the list of allowed/not-allowed ip addresses. This would allow for more efficiency and less repetitive tasks.&#x20;

### Entire code

<figure><img src="https://lh7-us.googleusercontent.com/GsvUmb7GYklO_bui22Up3sHbukz9vu2AmrLz6snQXZZYd14gQDyKtnPml5ypOIr2I5cxUuv19PkdXxR0BgPMGW8CK74tz6C0O7qvPHkB-1ASruz7Ct9_wk2jvmtg910up0c48IbVoydoKGYoKjUExrh4qBdH1VsXr_ts8-Tl1vI8qHa_dPHFC2ImxpTtdSM" alt=""><figcaption></figcaption></figure>

### Open the file that contains the allow list

import\_file = "allow\_list.txt"

### Read the file contents

with open(import\_file, "r") as file:

&#x20;   ip\_addresses = file.read()

### Convert the string into a list

ip\_addresses = ip\_addresses.split()

### Remove IP addresses that are on the remove list

remove\_list = \["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

for element in ip\_addresses:

&#x20;   if element in remove\_list:

&#x20;       ip\_addresses.remove(i)

### Update the file with the revised list of IP addresses&#x20;

ip\_addresses = " ".join(ip\_addresses)

with open(import\_file, "w") as file:

&#x20;   file.write(ip\_addresses)

\
\
\
