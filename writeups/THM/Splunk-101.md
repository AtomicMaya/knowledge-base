# Splunk 101

For this box I used the on-platform interface.

Link: [Splunk 101 Room on TryHackMe](https://tryhackme.com/room/splunk101)

## Task 1

### Question 1

Virtual machine deployed.

Answer: `No answer needed`

## Task 2

Go to the Start Menu, find Splunk, start it.

### Question 1

I'm ready to look at Splunk apps.

Answer: `No answer needed`

## Task 3

### Question 1

What is the 'Folder name' for the add-on?

After adding the plugin as described, we look at the Apps page.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/3.1.png?raw=true)

Answer: `TA-microsoft-sysmon`

### Question 2

What is the Version?

Answer: `10.6.2`

## Task 4

### Question 1

Upload the Splunk tutorial data on the desktop. How many events are in this source?

Note: Make sure you upload the data once only.

When uploading the data, select `Automatic` and, since it is on a Windows box, make sure to set `Host` to `Regular Expression on Path` and the test be ` \\(.*)\/`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/4.1-1.png?raw=true)
![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/4.1-2.png?raw=true)

Answer: `109,864`

## Task 5

### Question 1

Use Splunk to Search for the phrase 'failed password' using tutorialdata.zip as the source.

`* "failed password"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/5.1.png?raw=true)

Answer: `No answer needed` 

### Question 2

What is the sourcetype?

Answer: `www1/secure`

### Question 3

In the search result, look at the Patterns tab. 

Answer: `No answer needed`

### Question 4

What is the last username in this tab?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/5.4.png?raw=true)

Answer: `myuan`

### Question 5

Search for failed password events for this specific username. How many events are returned?

`* "failed password" myuan`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/5.5.png?raw=true)

Answer: `16`

## Task 6

Go to [Uncoder.io](https://uncoder.io)

### Question 1

Use the Select document feature. What is the Splunk query for 'sigma: APT29'?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/6.1.png?raw=true)

Answer: `CommandLine="*-noni -ep bypass $$*"`

### Question 2

Use the Github Sigma repo. What is the Splunk query for 'CACTUSTORCH Remote Thread Creation'?

Go to the [GitHub repo](https://github.com/SigmaHQ/sigma) and go to `rules/windows/create_remote_thread/sysmon_cactustorch.yml`.

Copy the text over to [Uncoder.io](https://uncoder.io), press translate to `Splunk`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/6.2.png?raw=true)

Answer: `(SourceImage="*\\System32\\cscript.exe" OR SourceImage="*\\System32\\wscript.exe" OR SourceImage="*\\System32\\mshta.exe" OR SourceImage="*\\winword.exe" OR SourceImage="*\\excel.exe") TargetImage="*\\SysWOW64\\*" NOT StartModule="*"`

## Task 7

### Question 1

Go to Dashboards -> Create new dashboard.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/7.1-1.png?raw=true)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/7.1-2.png?raw=true)

What is the highest EventID?

Make sure to set the search time range to `All time`!

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk_101/7.1-3.png?raw=true)

Answer: `11`

## Task 8

### Question 1

I have a general understanding on how to create an alert in Splunk.

Answer: `No answer needed` 

## Task 9

### Question 1

I know the fundamentals of Splunk.

Answer: `No answer needed` 