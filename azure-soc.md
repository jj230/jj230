# Azure-SOC

## Building a SOC + Honeynet in Azure (Live Traffic)

[![Screenshot 2023-12-27 at 4 41 23 PM](https://private-user-images.githubusercontent.com/93885534/293115859-6e195d27-ee5a-40a8-95b0-5476f3e06b69.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMxMTU4NTktNmUxOTVkMjctZWU1YS00MGE4LTk1YjAtNTQ3NmYzZTA2YjY5LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWEzNWYzYmY1MGVlNTVjNjg2OTlkYjk1NjZmOTMyNmE2OWJlZmVlNzdiMThlMmZhMTdiNDc5MDljYTFjNmQ5MDQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.oOQQ59x657iE7bC0gHyYkMVAWtPWcM5X5kT-6YfpnFw)](https://private-user-images.githubusercontent.com/93885534/293115859-6e195d27-ee5a-40a8-95b0-5476f3e06b69.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMxMTU4NTktNmUxOTVkMjctZWU1YS00MGE4LTk1YjAtNTQ3NmYzZTA2YjY5LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWEzNWYzYmY1MGVlNTVjNjg2OTlkYjk1NjZmOTMyNmE2OWJlZmVlNzdiMThlMmZhMTdiNDc5MDljYTFjNmQ5MDQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.oOQQ59x657iE7bC0gHyYkMVAWtPWcM5X5kT-6YfpnFw)

### Introduction

In this project, I created a small honeynet in Azure. I then setup a Log Aanalytics workspace to ingest the resources' logs and connected that to Microsoft Sentinel. Within Sentinel, I built attack maps and trigger alerts. I initially set up the network so that all traffic was allowed through. After a 72 hour period (Friday afternoon - Monday afternoon), I analyzed the incidents and events in Sentinel, responded to them, and gathered the attack metrics. Next, I setup Azure to monitor the safety score of the network in comparison to NIST 800-53, then followed some of its recommendations for how to harden the environment. After hardening, I waited until the following weekend to take the after-hardening attack metrics, because I wanted to compare the metrics during similar traffic times.

The metrics I analyzed were:

* SecurityEvent (Windows Event Logs)
* Syslog (Linux Event Logs)
* SecurityAlert (Log Analytics Alerts Triggered)
* SecurityIncident (Incidents created by Sentinel)
* AzureNetworkAnalytics\_CL (Malicious Flows allowed into our honeynet)

### Architecture Before Hardening / Security Controls

[![Screenshot 2023-12-28 at 10 04 59 AM](https://private-user-images.githubusercontent.com/93885534/293254669-d4b719b9-7b92-4edf-bf27-0cfdcc15ade2.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTQ2NjktZDRiNzE5YjktN2I5Mi00ZWRmLWJmMjctMGNmZGNjMTVhZGUyLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdkMTEyZjExODhhZGU3ZDZmZmViYzY4NmU4NWM4N2Q5Yzc5MjcxZDFkZjdlZWJiMTBmZTVkZjUxM2FjNWI1YmImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.H2vTerJuj9Ijtaja6AOiP2o003bJlmJqdW0\_tj49THs)](https://private-user-images.githubusercontent.com/93885534/293254669-d4b719b9-7b92-4edf-bf27-0cfdcc15ade2.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTQ2NjktZDRiNzE5YjktN2I5Mi00ZWRmLWJmMjctMGNmZGNjMTVhZGUyLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTdkMTEyZjExODhhZGU3ZDZmZmViYzY4NmU4NWM4N2Q5Yzc5MjcxZDFkZjdlZWJiMTBmZTVkZjUxM2FjNWI1YmImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.H2vTerJuj9Ijtaja6AOiP2o003bJlmJqdW0\_tj49THs)

### Architecture After Hardening / Security Controls

[![Screenshot 2023-12-28 at 10 07 57 AM](https://private-user-images.githubusercontent.com/93885534/293254619-90cffa21-e1d6-4596-8644-c59b7a77b18d.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTQ2MTktOTBjZmZhMjEtZTFkNi00NTk2LTg2NDQtYzU5YjdhNzdiMThkLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZjMmEyZGRmYTI1M2Y2ZDM1ZDY3MTk4MjQ3ZDI1ZjMzOGQ0OGNkZjhlZjI5ZjIwMmY4ZjM3MzdkY2ZjNzE3NDcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.AFRVpdfoj9lGHFUytJIRyipD42Un0kf9cbAQT3DDy-U)](https://private-user-images.githubusercontent.com/93885534/293254619-90cffa21-e1d6-4596-8644-c59b7a77b18d.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTQ2MTktOTBjZmZhMjEtZTFkNi00NTk2LTg2NDQtYzU5YjdhNzdiMThkLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZjMmEyZGRmYTI1M2Y2ZDM1ZDY3MTk4MjQ3ZDI1ZjMzOGQ0OGNkZjhlZjI5ZjIwMmY4ZjM3MzdkY2ZjNzE3NDcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.AFRVpdfoj9lGHFUytJIRyipD42Un0kf9cbAQT3DDy-U)

The architecture of the mini honeynet in Azure consists of the following components:

* Virtual Network (VNet)
* Network Security Group (NSG)
* Virtual Machines (2 windows, 1 linux)
* Log Analytics Workspace
* Azure Key Vault
* Azure Storage Account
* Microsoft Sentinel

### BEFORE AND AFTER METRICS

For the "BEFORE" metrics, all NSGs and built-in firewalls were setup to be completely open to the interent. All other resources had visible public endpoints.

For the "AFTER" metrics, NSGs were hardened by blocking ALL traffic with the exception of my admin workstation. All other resources were protected by their built-in firewalls as well as Private Endpoints.

### Attack Maps Before Hardening / Security Controls

[![NSG-Malicious-Allowed-In (alltime)](https://private-user-images.githubusercontent.com/93885534/293250280-5b8bb2fb-ffc5-4aa0-a8c0-5aa3d60aa6ad.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAyODAtNWI4YmIyZmItZmZjNS00YWEwLWE4YzAtNWFhM2Q2MGFhNmFkLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWI2NmJjMGE5OWJmN2Y4OTMxMGFlNjU3MWM5YTc2NDUwMjNiZDEzNTA3NWRhNDQ0ZTEzOGIzMWVhMTVlYTM3YjImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.Ac3WYdvCwXurkq9TaQGtBSWWakfdG9wZE8ciBf2DnrA)](https://private-user-images.githubusercontent.com/93885534/293250280-5b8bb2fb-ffc5-4aa0-a8c0-5aa3d60aa6ad.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAyODAtNWI4YmIyZmItZmZjNS00YWEwLWE4YzAtNWFhM2Q2MGFhNmFkLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWI2NmJjMGE5OWJmN2Y4OTMxMGFlNjU3MWM5YTc2NDUwMjNiZDEzNTA3NWRhNDQ0ZTEzOGIzMWVhMTVlYTM3YjImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.Ac3WYdvCwXurkq9TaQGtBSWWakfdG9wZE8ciBf2DnrA)\
[![Linux\_SSH\_Auth\_Fail (all time?)](https://private-user-images.githubusercontent.com/93885534/293250333-248fdc7a-5286-4c7c-aead-434d843dd970.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAzMzMtMjQ4ZmRjN2EtNTI4Ni00YzdjLWFlYWQtNDM0ZDg0M2RkOTcwLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTU5ZDllZTQzOTkyMDE2OGFjZjgzOGIxMmQ2OTNkYTRjZTk0NWQ3NmM1YjU0MDM3MTczYjZmZGZlZGIyYjlmZWQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.O3ms6kMH9V50ERRutwQI21LOs1PH-L4gJmvVywwNfyI)](https://private-user-images.githubusercontent.com/93885534/293250333-248fdc7a-5286-4c7c-aead-434d843dd970.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAzMzMtMjQ4ZmRjN2EtNTI4Ni00YzdjLWFlYWQtNDM0ZDg0M2RkOTcwLmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTU5ZDllZTQzOTkyMDE2OGFjZjgzOGIxMmQ2OTNkYTRjZTk0NWQ3NmM1YjU0MDM3MTczYjZmZGZlZGIyYjlmZWQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.O3ms6kMH9V50ERRutwQI21LOs1PH-L4gJmvVywwNfyI)\
[![Windows-RDP-Auth-Fail (alltime?)](https://private-user-images.githubusercontent.com/93885534/293250370-9852eeac-bc84-490f-8e17-331bfccee7d8.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAzNzAtOTg1MmVlYWMtYmM4NC00OTBmLThlMTctMzMxYmZjY2VlN2Q4LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTc4NGMxZTNjZGYyYTBjZGUzZDlhYTRkZmYxNWNjMDIxZTc5OTVhMGI0MTMzOTZjOTVkZjc3ODVmM2FmZDYxOTYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.k54gmBKypmLy2oAUaDqWDUnlz81Z63niCBgdH7ZsElw)](https://private-user-images.githubusercontent.com/93885534/293250370-9852eeac-bc84-490f-8e17-331bfccee7d8.jpg?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MDQ3NjI3OTgsIm5iZiI6MTcwNDc2MjQ5OCwicGF0aCI6Ii85Mzg4NTUzNC8yOTMyNTAzNzAtOTg1MmVlYWMtYmM4NC00OTBmLThlMTctMzMxYmZjY2VlN2Q4LmpwZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAxMDklMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMTA5VDAxMDgxOFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTc4NGMxZTNjZGYyYTBjZGUzZDlhYTRkZmYxNWNjMDIxZTc5OTVhMGI0MTMzOTZjOTVkZjc3ODVmM2FmZDYxOTYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.k54gmBKypmLy2oAUaDqWDUnlz81Z63niCBgdH7ZsElw)\


### Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:

Day 1: Friday -> Saturday

| Metric     | Time (EST)            |
| ---------- | --------------------- |
| Start Time | 12/8/2023, 4:23:11 PM |
| Stop Time  | 12/9/2023, 4:23:11 PM |

| Metric                    | Count |
| ------------------------- | ----- |
| SecurityEvent             | 76895 |
| Syslog                    | 18629 |
| SecurityAlert             | 1     |
| SecurityIncident          | 238   |
| AzureNetworkAnalytics\_CL | 3270  |

Day 2: Saturday -> Sunday

| Metric     | Time (EST)             |
| ---------- | ---------------------- |
| Start Time | 12/9/2023, 4:23:11 PM  |
| Stop Time  | 12/10/2023, 4:23:11 PM |

| Metric                    | Count  |
| ------------------------- | ------ |
| SecurityEvent             | 137187 |
| Syslog                    | 18163  |
| SecurityAlert             | 13     |
| SecurityIncident          | 241    |
| AzureNetworkAnalytics\_CL | 5050   |

Day 3: Sunday -> Monday

| Metric     | Time (EST)             |
| ---------- | ---------------------- |
| Start Time | 12/10/2023, 4:23:11 PM |
| Stop Time  | 12/11/2023, 4:23:11 PM |

| Metric                    | Count |
| ------------------------- | ----- |
| SecurityEvent             | 24331 |
| Syslog                    | 36363 |
| SecurityAlert             | 8     |
| SecurityIncident          | 237   |
| AzureNetworkAnalytics\_CL | 5307  |

### Attack Maps Before Hardening / Security Controls

`All map queries returned no results due to no documented instances of malicious activity for the 72 hour period after hardening.`

### Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:

Day 1: Friday -> Saturday

| Metric     | Time (EST)             |
| ---------- | ---------------------- |
| Start Time | 12/15/2023, 4:49:51 PM |
| Stop Time  | 12/16/2023, 4:49:51 PM |

| Metric                    | Count |
| ------------------------- | ----- |
| SecurityEvent             | 11295 |
| Syslog                    | 0     |
| SecurityAlert             | 0     |
| SecurityIncident          | 0     |
| AzureNetworkAnalytics\_CL | 0     |
| Malicious Flows Denied    | 3259  |

Day 2: Saturday -> Sunday

| Metric     | Time (EST)             |
| ---------- | ---------------------- |
| Start Time | 12/16/2023, 4:49:51 PM |
| Stop Time  | 12/17/2023, 4:49:51 PM |

| Metric                    | Count |
| ------------------------- | ----- |
| SecurityEvent             | 8337  |
| Syslog                    | 0     |
| SecurityAlert             | 0     |
| SecurityIncident          | 0     |
| AzureNetworkAnalytics\_CL | 0     |
| Malicious Flows Denied    | 2708  |

Day 3: Sunday -> Monday

| Metric     | Time (EST)             |
| ---------- | ---------------------- |
| Start Time | 12/17/2023, 4:49:51 PM |
| Stop Time  | 12/18/2023, 4:49:51 PM |

| Metric                    | Count |
| ------------------------- | ----- |
| SecurityEvent             | 8172  |
| Syslog                    | 0     |
| SecurityAlert             | 0     |
| SecurityIncident          | 0     |
| AzureNetworkAnalytics\_CL | 0     |
| Malicious Flows Denied    | 2399  |

### Results

| Metric                    | Change after hardening |
| ------------------------- | ---------------------- |
| Security Events           | -66.41%                |
| Syslog                    | -100.00%               |
| SecurityAlert             | -100.00%               |
| Security Incident         | -100.00%               |
| AzureNetworkAnalytics\_CL | -100.00%               |

### Reflections

I learned through this project how to set up a network on Azure, including VMs, NSGs, Log Analytics, Microsoft Sentinel, and Entra ID. I learned how to create different workbooks and attack maps based on incoming incidents. I learned to use KQL and sort through thousands of logs. I practiced responding to incidents and remediating them. I also learned to work with and apply security recommendations, specifically with NIST 800-53.

This project shows how important even the smallest steps are to hardening an environment. Only minimal hardening steps were taken, but the results were dramatic. For a network with higher needs, valuable resources, and sensitive information, I would certainly want to secure the environment further. The Azure environment was fully setup for me to easily take those next steps to secure the environment even more if need be. I also could have added different recommendations to the environment to check against those.

### Opportunities for Further Learning

I would like to better understand why there are still security events after hardening: what are they, how could I stop them, and why didn't they show up on the maps. Now that I have a good visualization for this project, I would be curious to re-create this lab a 2nd time to more deeply understand it and to experiment with applying more of the NIST 800-53 recommendations.
