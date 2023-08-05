# Microsoft Sentinel SIEM

![AZ](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/67beb882-e81e-44c9-9211-d99c577ce189)

<h1>Setting Up Azure Sentinel</h1>

1. First you need to create a free Azure account (https://azure.microsoft.com/en-us/free/)

2. Create the Virtual Machine and Network Security Group

<img width="1792" alt="1  NSG creation" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/29fcccf6-1b5e-45b7-9170-c65ccf733795">

<img width="1792" alt="2  Resource Group   VM " src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/4515582d-13d8-4df5-914d-6933e1e3e680">


<h2>Create Log Analytics Workspace</h2>

1. Search "Log Analytics Workspace"

<img width="1792" alt="3  Log Analytics Creation" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/a196f60f-3d7f-46f2-9e5e-ed8671673cbb">

2. Go to "Microsoft Defender for Cloud"
  - Go to "Enviornment Settings" then select your honeypot.
  - Turn off Azure Defender for "SQL Servers on Machines"
  - Got to datacollection and change the option to "All Events"

<img width="1792" alt="4  Microsoft Defender" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/a8ce8063-ba2a-4950-a4f7-92e10b2ea298">

<img width="1792" alt="5  Defender Settings" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/79276c89-2a7a-4af1-bf4e-b6725547baf3">


3. Connect log Analytics to Virtual Machine

- Select your created workspace. Then go to "Virtual Machines" under "Workspace Data Sources".
- Select the VM then hit the connect button.

<img width="1792" alt="7" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/0d783528-35eb-4f19-9b98-009f3d44c011">

<img width="994" alt="8  Coonecting WorkSpace" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/cc4a8564-fd72-4eea-ad87-173aa249d2de">


<h3>Mircrosoft Sentinel Setup</h3>

- Search for "Microsoft Sentinel"
- Your created workspace will appear. Select it and add sentential.

<img width="1792" alt="9  Microsoft Sentinal" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/4684dceb-c269-4ff7-8569-f8ce4b8d5a08">

<h4>Log into VM via Remote Desktop</h4>

- Go to your VM and retrieve the IP address 
- Login and fail one attempt (This forms an incident on the log)
- 






