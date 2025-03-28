# Exploring and Managing System Event Logs with PowerShell

This lab focuses on utilizing PowerShell to explore, analyze, and manage system event logs. Event logs provide valuable insights into system performance, security incidents, and application behavior, making them essential for troubleshooting and system administration. PowerShell offers a powerful and efficient way to retrieve, filter, and automate log management tasks.<br/>

<h2>Environments Used </h2>

- <b>Hyper-V</b>
- <b>Windows Server 2016</b>
- <b>Windows 11</b>

***Open PowerShell as Administrator***
- Press Windows Key + X and select Windows PowerShell (Admin) or PowerShell (Admin).
- If prompted by User Account Control (UAC), click Yes to allow the app to make changes to your device.

Using PowerShell to View Event Logs
2. Get Event Logs from Different Categories
Use the Get-EventLog cmdlet to retrieve event logs.

Get-EventLog -LogName Application
Get-EventLog -LogName System
Get-EventLog -LogName Security
<p align="center">
<br/>
<img src="https://imgur.com/rHJ8rsw.png .png" height="65%" width="65%" alt>
<br />
<br />
 <br />
<img src="https://imgur.com/GgVHgGw.png" height="65%" width="65%" alt>
<br />
<br />
<img src="https://imgur.com/Ho7sCZn.png" height="65%" width="65%" alt>
<br />
<br />
 <br />
<img src="https://imgur.com/liG1qx0.png" height="65%" width="65%" alt>
<br />
<br />
<img src="https://imgur.com/01hwmmI.png" height="65%" width="65%" alt>
<br />
<br />
 <br />
<img src="https://imgur.com/1df01cg.png" height="65%" width="65%" alt>

***Did the large number of results from the event logs occur because they encompass the entire lifespan of the computer?***

Yes, the reason `Get-EventLog -LogName Application`, `Get-EventLog -LogName System`, and `Get-EventLog -LogName Security` return thousands of results is primarily because the event logs accumulate data over the lifetime of the computer. These logs capture various system, application, and security-related events that occur continuously. If the logs are not cleared or managed regularly, the accumulated data can become quite large.

***Note***: The logs do not automatically clear on their own. If log size limits are set the older records will be overwritten still returning thousands of records. To clear the records you will use cmdlet: Clear-EventLog -LogName Application
Clear-EventLog -LogName System
Clear-EventLog -LogName Security

Filtering Event Logs
Filter by Event Type (e.g., Errors):
To make the data easier to read filtering the results can remove the information not needed:
Get-EventLog -LogName Application -EntryType Error

Filter by Event Source (e.g., “Service Control Center”
Get-EventLog -LogName System -Source "Service Control Manager"

Filter by Date (e.g., logs from the past 7 days):
Get-EventLog -LogName Application -After (Get-Date).AddDays(-7)
<br />
 <br />
<br/>
<img src="https://imgur.com/I5ZO4x8.png" height="65%" width="65%" alt>
<br />
<br />
<img src="https://imgur.com/nAQ2oZY.png" height="65%" width="65%" alt>
<br />
<br />
 <br />
<img src="https://imgur.com/0UKREbm.png" height="65%" width="65%" alt>
  
Filtering the event specifically by the type made the list not as long rather than combining them all at once. Now, the can be exported into a .CSV file, which can be much easier to review and share with others who need to see the logs.

Get-EventLog -LogName Application -EntryType Error | Export-Csv -Path "C:\Logs\error_logs.csv" -NoTypeInformation
<br />
 <br />
<br/>
<img src="https://imgur.com/yJbzqpX.png" height="65%" width="65%" alt>
<br />
<br />
The spreadsheet was sent to the requested folder and is now ready for review.
<br />
<br />
<img src="https://imgur.com/kRJa9cN.png" height="130%" width="130%" alt>
 
In this lab, system event logs were explored and managed using PowerShell. Key tasks included retrieving event logs from various categories, filtering logs based on criteria such as error types or event sources, exporting logs for further analysis, and clearing logs when necessary. These skills are essential for maintaining system health, troubleshooting issues, and ensuring that systems run smoothly.


