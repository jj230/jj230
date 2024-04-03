# Attack Port(s) Search

I created this script while working on answering questions about a brute force login attack based on a log file in csv format. I needed to find the highest and lowest port numbers that an attacker was attacking from. I had the idea of creating a python script that would help me do this.

Relying on what I know about python and scripts already mixed with some research, I created this script in about a half hour to successfully find the specific ports, the range of ports, and the number of different ports used that were attacking a system.

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/c431a7cb-5683-4bc9-acab-14fbbaee0002" width = "650">

</div>

The resulting output showed the attempted logins to be from 3103 different ports in the range: 49162-65534.

I updated the script further to also reveal the source IP Address(es). 

<div align="left">

<img src="https://github.com/jj230/jj230/assets/93885534/d1c2e9e6-a3dc-418b-b246-56742a6a4ba8" width = "650">

</div>

# Analysis

In normal web traffic, an ephemeral source port is used for initial connection. Once that connection is made, the ephemeral port stays the same. In the case of failed login attempts, the connection is normally maintained between failed login attempts, which would mean the chosen source port would remain the same. The change of ephemeral source ports could be an attempt by the attacker to obfuscate their brute force attack. By changing their source port, they start a new connection each time and may make it harder for systems to catch them. 

# Sentinel Rule to Alert to Traffic of this Kind

This type of rule would need fine-tuning over time. For instance, it can be updated to rule out known, trusted traffic, and the threshold could change based on number of false positives. 

SecurityEvent 
| where TimeGenerated > ago(5min)  // Adjust time window as needed
| summarize ConnectionCount = count(), DistinctSourcePorts = dcount(DestinationPort) by SourceIP
| where DistinctSourcePorts > 100 // Adjust threshold as needed

