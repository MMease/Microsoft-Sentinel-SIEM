# Microsoft Sentinel SIEM

![AZ](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/67beb882-e81e-44c9-9211-d99c577ce189)

<h1>Setting Up Azure Sentinel</h1>

1. First you need to create a free Azure account (https://azure.microsoft.com/en-us/free/)

2. Create the Virtual Machine and Network Security Group

<img width="1792" alt="1  NSG creation" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/29fcccf6-1b5e-45b7-9170-c65ccf733795">

<img width="1792" alt="2  Resource Group   VM " src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/4515582d-13d8-4df5-914d-6933e1e3e680">


<h1>Create Log Analytics Workspace</h2>

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


<h1>Mircrosoft Sentinel Setup</h3>

- Search for "Microsoft Sentinel"
- Your created workspace will appear. Select it and add sentential.

<img width="1792" alt="9  Microsoft Sentinal" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/4684dceb-c269-4ff7-8569-f8ce4b8d5a08">

<h1>Log into VM via Remote Desktop</h4>

- Go to your VM and retrieve the IP address 
- Login and fail one attempt (This forms an incident on the log)
- Observe Event Viewer Logs in VM
- Next, Gather infromation about the IP address (https://ipgeolocation.io)

<img width="1792" alt="10  Event Viewer" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/f3df49ac-0a57-4b7b-9259-55d0157de02f">


<h1>Make System Discoverable Online</h5>

- On your local Computer, Open the Command Terminal
  - Use " Ping (VMs Public IP) -t
  - This is a perpetual ping

- Next, Go to your VM and disable the Firewall
  - Type "wf.msc" in your home search bar
  - Select "Windows Defender Firewall Properties"
  - Turn off firewall state for "Domain, Private, & Public" profiles
  - Go back to your local machine command terminal. The ping should start working.
 
<h1>Github Script & Retrieve API Key</h1>

- Download Powershell Script (https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1)
- Open "Windows Powershell ISE" and Copy the Code into the a new script.
- Retrieve an API Key from https://ipgeolocation.io
  - Create an account. When you're finished you will receive a key.
  - Copy that Key and Paste it into the Powershell script.
  - Now that you have your own API key. You can run the script
  - You may encounter errors. Don't worry it will still work‼️
  - A file named "Failed_RDP" will be created

<img width="1597" alt="Powershell Script" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/a55fdd85-8c5a-4c84-970d-22991933b189">

<img width="1327" alt="Failed_RDP" src="https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/5c260c72-9750-4015-ba8e-98ef6565868f">


<h1>Create custom log in LAW to bring in our custom log</h1>

- In Azure portal go to "Log Analytics Workspace"
- Select your created workspace
- Go to Tables & select "New custom log (DCR-based)"
- Copy the contents of your "Failed_RDP" file & and copy it onto your local machine. Then select that file for your log.
- Follow the process. Review and create log once everything is checked.

![LAW Logs](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/66b6caa0-8ed8-4851-8d87-2c961f6e583b)

<h1>Setup map in sentinel with Data</h1>

- Go to "Azure Sentinel"
- Select your workspace. Under the "Threat Managment" tab select Workbooks then select edit.
- Remove the initial widgets that comes with the workbook
  - Go to "add" then "add query". Copy & paste the following code:


FAILED_RDP_WITH_GEO_CL

| parse RavData with * "latitude:" Latitude ", Longitude:" Longitude ", destinationhost:" DestinationHost ", username:" Username ", sourcehost:" Sourcehost ", state:" State ", country:" Country ", label:" Label ", timestamp:" Timestamp

| where DestinationHost != "samplehost"

| where Sourcehost != ""

| summarize event_count=count () by Sourcehost, Latitude, Longitude, Country, Label, DestinationHost

- After you finish the code. Run the query and select "Map" for visualization.

- Your data when begin to plot and you're all done.
  
![Sentinel Query Code](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/47e375b4-5d6d-410a-b00f-fb5ace31804d)

![World Map](https://github.com/MMease/Microsoft-Sentinel-SIEM/assets/42321472/e947720c-15f2-4f99-83a6-175fed62f7cf)

<b>ENSURE ALL RESOURCES ARE DELETED WHEN FINISHED‼️</b>
