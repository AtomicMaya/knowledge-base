# Investigating Windows

For this box I used the browser based remote.

Link: [Investigating Windows Room on TryHackMe](https://tryhackme.com/room/investigatingwindows)

## Task 1

### Question 1

What's the version and year of the windows machine?

Go to `Settings -> System -> About`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/1.png?raw=true)

Answer: `Windows Server 2016`

### Question 2

Which user logged in last?

We can go to the `EventViewer -> WindowsLogs -> Security` and scroll to all events predating the date where you're logging into the box.

If we look at the Logoff event, we can see the Account Name.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/2.png?raw=true)

Answer: `Administrator`

### Question 3

When did John log onto the system last? Answer format: MM/DD/YYYY H:MM:SS AM/PM

In the same logs, we can filter by any `Task Category` being `Logoff`, but this doesn't lead us to the correct result.

If we open `cmd`, we can use the `net user` command to find the fully qualified user name (`John`) and then find the last logon using:

`net user John | findstr "Last"` 

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/3.png?raw=true)

Answer: `03/02/2019 5:48:32 PM`

### Question 4

What IP does the system connect to when it first starts?

I actually had to reboot the machine to grab the following screenshot, but it was worth it.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/4.png?raw=true)

Answer: `10.34.2.3`

### Question 5

What two accounts had administrative privileges (other than the Administrator user)? Answer format: username1, username2

We can expand upon the netuser command and filter for groups using `net user $USER | findstr "Local Group"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/5.png?raw=true)

Answer: `Guest, Jenny`

### Question 6

What's the name of the scheduled task that is malicious.

We can go to the Task Scheduler and look through the scheduled tasks.

One of them stands out by launching a process in `C:/TMP`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/6.png?raw=true)

Answer: `clean file system`

### Question 7

What file was the task trying to run daily?

From the previous image.

Answer: `nc.ps1`

### Question 8

What port did this file listen locally for?

From the previous image.

Answer: `1348`

### Question 9

When did Jenny last logon?

`net user Jenny | findstr "Last"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/9.png?raw=true)

Answer: `Never`

### Question 10

At what date did the compromise take place? Answer format: MM/DD/YYYY

If we look further at the `C:/TMP` directory, we can look at the modification date of the files.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/10.png?raw=true)

Answer: `03/02/2019`

### Question 11

At what time did Windows first assign special privileges to a new logon? Answer format: MM/DD/YYYY HH:MM:SS AM/PM

If we look at the event logs on that date, we can see a lot of activity around `4:04:47`, including a suspicious system time blip, started by `rundll32.exe`:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/11-1.png?raw=true)

The next special logon is at `4:04:49 PM`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/11-2.png?raw=true)

Answer: `03/02/2019 04:04:49 PM`

### Question 12

What tool was used to get Windows passwords?

If we look at the files within `C:/TMP` we can see a `mim-out.txt` file, which if opened shows `mimikatz(powershell)`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/12.png?raw=true)

Answer: `mimikatz`

### Question 13

What was the attackers external control and command servers IP?

If we look at the `C:/Windows/System32/drivers/etc/hosts` file, we can see that a lot of IP's are rerouted to localhost or to other IPs:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/13.png?raw=true)

The only nonstandard IP is the one in `76.x.x.x` and is tied to the domain in question for question 16.

Answer: `76.32.97.132`

### Question 14

What was the extension name of the shell uploaded via the servers website?

If we look in `C:/inetpub/wwwroot`, we can see `*.jsp` files.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/14.png?raw=true)

Answer: `.jsp`

### Question 15

What was the last port the attacker opened?

If we look at the Firewall Inbound rules, we can see a rule "for development", on port 1337.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/15.png?raw=true)

Answer: `1337`

### Question 16

Check for DNS poisoning, what site was targeted?

Beyond what we saw in question 13, if we look at `C:/TMP/schtasks.backdoor.ps1`, we can see requests being made to `8.8.8.8`, which is the IP address for Google.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/investigating_windows/16.png?raw=true)

Answer: `google.com`