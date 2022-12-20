# Windows Event Logs

For this box I used Remmina on Kali Linux while connected to the TryHackMe VPN.

Link: [Windows Event Logs Room on TryHackMe](https://tryhackme.com/room/windowseventlogs)

## Task 1

### Question 1

Let's begin...

Answer: `No answer needed`

## Task 2

### Question 1

For the questions below, use Event Viewer to analyze Microsoft-Windows-PowerShell/Operational log.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.1-1.png?raw=true)
![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.1-2.png?raw=true)

Answer: `No answer needed`

### Question 2

What is the Event ID for the first event?

Scroll to the bottom to find it.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.2.png?raw=true)

Answer: `40961`

### Question 3

Filter on Event ID 4104. What was the 2nd command executed in the PowerShell session?

Create a filter on the event ID.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.3-1.png?raw=true)

Then scroll to the bottom and take the second element.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.3-2.png?raw=true)

Answer: `whoami`

### Question 4

What is the Task Category for Event ID 4104?

Answer: `Execute a remote command`

### Question 5

For the questions below, use Event Viewer to analyze the Windows PowerShell log.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.5.png?raw=true)

Answer: `No answer needed`

### Question 6

What is the Task Category for Event ID 800?

Filter on Event ID 800.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/2.6.png?raw=true)

Answer: `Pipeline Execution Details`

## Task 3

### Question 1

How many log names are in the machine? 

`wevtutil.exe el | Measure-Object`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.1.png?raw=true)

Answer: 1071

### Question 2

What is the definition for the query-events command?

`wevtutil.exe qe /?`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.2.png?raw=true)

Answer: `Read events from an event log, log file or using structured query.`

### Question 3

What option would you use to provide a path to a log file?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.3.png?raw=true)

Answer: `/lf:true`

### Question 4

What is the VALUE for /q?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.4.png?raw=true)

Answer: `XPATH query`

### Question 5

The questions below are based on this command: `wevtutil qe Application /c:3 /rd:true /f:text`

Answer: `No answer needed`

### Question 6

What is the log name?

Answer: From the query, the log name is `Application`

### Question 7

What is the /rd option for?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.7.png?raw=true)

Answer: `Event read direction`

### Question 8

What is the /c option for?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/3.8.png?raw=true)

Answer: `Maximum number of events to read`

## Task 4

### Question 1

Answer the following questions using the [online](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.diagnostics/Get-WinEvent?view=powershell-7.1) help documentation for Get-WinEvent

Answer: `No answer needed`

### Question 2

Execute the command from Example 1 (as is). What are the names of the logs related to OpenSSH?

`Get-WinEvent -ListLog *`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/4.2.png?raw=true)

Answer: `OpenSSH/Admin,OpenSSH/Operational`

### Question 3

Execute the command from Example 7. Instead of the string `*Policy*` search for `*PowerShell*`. What is the name of the 3rd log provider?

`Get-WinEvent -ListProvider *Powershell*`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/4.3.png?raw=true)

Answer: `Microsoft-Windows-PowerShell-DesiredStateConfiguration-FileDownloadManager`

### Question 4

Execute the command from Example 8. Use Microsoft-Windows-PowerShell as the log provider. How many event ids are displayed for this event provider?

`(Get-WinEvent -ListProvider Microsoft-Windows-PowerShell).Events | Format-Table Id, Description  | Measure-Object`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/4.4.png?raw=true)

Answer: `192`

### Question 5

How do you specify the number of events to display?

Answer: `-MaxEvents`

### Question 6

How do you specify the number of events to display?

Answer: `4`

## Task 5

### Question 1

Using Get-WinEvent and XPath, what is the query to find WLMS events with a System Time of 2020-12-15T01:09:08.940277500Z?

Answer: `Get-WinEvent -LogName Application -FilterXPath '*/System/Provider[@Name="WLMS"] and */System/TimeCreated[@Name="SystemTime"]="2020-12-15T01:09:08.940277500Z"'`

### Question 2

Using Get-WinEvent and XPath, what is the query to find a user named Sam with an Logon Event ID of 4720?

Answer: `Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="Sam" and */System/EventID=4720'`

### Question 3

Based on the previous query, how many results are returned?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/5.3.png?raw=true)

Answer: `2`

### Question 4

Based on the output from the question #2, what is Message?

Answer: `A user account was created`

### Question 5

Still working with Sam as the user, what time was Event ID 4724 recorded? (MM/DD/YYYY H:MM:SS [AM/PM])

`Get-WinEvent -LogName Security -FilterXPath '*/EventData/Data[@Name="TargetUserName"]="Sam" and */System/EventID=4724'`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/5.5.png?raw=true)

Answer: `12/17/2020 1:57:14 PM`

### Question 6

What is the Provider Name?

Answer: `Microsoft-Windows-Security-Auditing`

## Task 6

### Question 1

I'm ready to look at some event logs...

Answer: `No answer needed`

## Task 7

### Question 1

What event ID is to detect a PowerShell downgrade attack?

Answer: From a bit of research, I stumbled upon [this website](https://www.leeholmes.com/detecting-and-preventing-powershell-downgrade-attacks/) which puts the "classic" event ID at `400`

### Question 2

What is the Date and Time this attack took place? (MM/DD/YYYY H:MM:SS [AM/PM])

`Get-WinEvent -Path .\merged.evtx -FilterXPath '*/System/EventID=400'`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/7.2.png?raw=true)

Answer: `12/18/2020 7:50:33 AM`

### Question 3

A Log clear event was recorded. What is the 'Event Record ID'?

By going to the EventViewer and filtering by `Task Category` we can find a single `Log Clear` event. When moving to the `Details` pane and selecting `XML View` (or unpacking system in the `Friendly View`) we obtain our answer.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/7.3.png?raw=true)

Answer: `27736`

### Question 4

What is the name of the computer?

Same view as before, but under `Computer`.

Answer: `PC01.example.corp`

### Question 5

What is the name of the first variable within the PowerShell command?

(From the instructions we are advised to search for event ID 4104 and the text "ScriptBlockText" within the EventData element).

`Get-WinEvent -Path .\merged.evtx -FilterXPath '*/EventData/Data[@Name="ScriptBlockText"] and */System/EventID=4104' -Oldest -MaxEvents 1 | Format-List`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/7.5.png?raw=true)

Answer: `$Va5w3n8`

### Question 6

What is the Date and Time this attack took place? (MM/DD/YYYY H:MM:SS [AM/PM])

Answer: `8/25/2020 10:09:28 PM`

### Question 7

What is the Execution Process ID?

In the Event Viewer, we can filter by Event ID 4104, and then go down to the oldest event, in the XML view lies our answer.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/7.7.png?raw=true)

Answer: `6620`

### Question 8

What is the Group Security ID of the group she enumerated?

First, we find the event ID, by googling, which [brings us](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4799) to event ID 4799. 

This is also the answer to Question 9.

`Get-WinEvent -Path .\merged.evtx -FilterXPath '*/System/EventID=4799' -Oldest -MaxEvents 1 | Format-List`

This gets us the following:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/windows_event_logs/7.8.png?raw=true)

Answer: `S-1-5-32-544`

### Question 9

Answer: `4799`

## Task 8

### Question 1

Hope you enjoyed this room and learned a thing or two.

Answer: `No answer needed`