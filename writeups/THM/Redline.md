# Redline

For this box I used the browser based remote.

Link: [Redline on TryHackMe](https://tryhackme.com/room/btredlinejoxr3d)

## Task 1

### Question 1

Who created Redline?

Answer: `FireEye`

## Task 2

### Question 1

What data collection method takes the least amount of time?

Answer: `Standard Collector`

### Question 2

You are reading a research paper on a new strain of ransomware. You want to run the data collection on your computer based on the patterns provided, such as domains, hashes, IP addresses, filenames, etc. What method would you choose to run a granular data collection against the known indicators?

Answer: `IOC Search Collector`

### Question 3

What script would you run to initiate the data collection process? Please include the file extension.

Answer: `RunRedlineAudit.bat`

### Question 4

If you want to collect the data on Disks and Volumes, under which option can you find it? 

Answer: `Disk Enumeration`

### Question 5

What cache does Windows use to maintain a preference for recently executed code? 

From [the Redline User Guide](https://www.fireeye.com/content/dam/fireeye-www/services/freeware/ug-redline.pdf)

Answer: `Prefetch`

## Task 3

### Question 1

Where in the Redline UI can you view information about the Logged in User?

Answer: `System Information`

## Task 4

(Setting up the machine takes an unimaginable amount of time - 25 minutes)

### Question 1

Provide the Operating System detected for the workstation.

Go to the `System Information` tab and scroll down.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/4.1.png?raw=true)

Answer: `Windows Server 2019 Standard 17763`

### Question 2

Provide the BIOS Version for the workstation.

Answer: `Xen 4.2.amazon`

### Question 3

What is the suspicious scheduled task that got created on the victim's computer?

Go to the `Tasks` tab and look around for weird names.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/4.3.png?raw=true)

Answer: `MSOfficeUpdateFa.ke`

### Question 4

Find the message that the intruder left for you in the task.

Answer: `THM-p3R5IStENCe-m3Chani$m`

### Question 5

There is a new System Event ID created by an intruder with the source name "THM-Redline-User" and the Type "ERROR". Find the Event ID #.

By going to the `Event Logs` tab and filtering for `THM-Redline-User` in the `Source` category, we get exactly one match:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/4.5.png?raw=true)

Answer: `546` 

### Question 6

Provide the message for the Event ID.

Answer: `Someone cracked my password. Now I need to rename my puppy-++-`

### Question 7

It looks like the intruder downloaded a file containing the flag for Question 8. Provide the full URL of the website.

We can go to the `File Download History` tab and look for any fishy looking downloads:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/4.7.png?raw=true)

Answer: `https://wormhole.app/download-stream/gI9vQtChjyYAmZ8Ody0AuA`

### Question 8

Provide the full path to where the file was downloaded to including the filename.

Answer: `C:\Program Files (x86)\Windows Mail\SomeMailFolder\flag.txt`

### Question 9

Provide the message the intruder left for you in the file.

Manually navigate to the correct folder using File Explorer and open it in Notepad:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/4.9.png?raw=true)

Answer: `THM{600D-C@7cH-My-FR1EnD}`

## Task 5

### Question 1

What is the actual filename of the Keylogger?

Given in the exercise.

Answer: `psylog.exe`

### Question 2

What filename is the file masquerading as? 

From the file with the most amount of hits, we can gather some information:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/5.2.png?raw=true)

Answer: `THM1768.exe`

### Question 3

Who is the owner of the file? 

Answer: `WIN-2DET5DP0NPT\charles`

### Question 4

What is the file size in bytes? 

Answer: `35400`

### Question 5

Provide the full path of where the .ioc file was placed after the Redline analysis, include the .ioc filename as well.

From the initial Analysis report pane, we can see the following:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/5.5.png?raw=true)

Answer: `C:\Users\charles\Desktop\Keylogger-IOCSearch\IOCs\keylogger.ioc` 

## Task 6

From the THM Discord:
```txt
There is discussion for a solution (on reddit i think). Basically you need to create an IoC report from the existing scan on the machine ( C:\Users\Administrator\Documents\Analysis\Sessions\AnalysisSession1), creating a new IoC search collector doesn't work.
```

### Question 1

Provide the path of the file that matched all the artifacts along with the filename.

If we look at the IOC, we find a single match:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/6.1.png?raw=true)

Answer: `C:\Users\Administrator\AppData\Local\Temp\8eJv8w2id6lqN85dfC.exe`

### Question 2

Provide the path where the file is located without including the filename.

Answer: `C:\Users\Administrator\AppData\Local\Temp`

### Question 3

Who is the owner of the file?

Answer: `BUILTIN\Administrators`

### Question 4

Provide the subsystem for the file.

Answer: `WINDOWS_CUI`

### Question 5

Provide the Device Path where the file is located.

Answer: `\Device\HarddiskVolume2`

### Question 6

Provide the hash (SHA-256) for the file.

The hash for the file can be retrieved with the `Get-FileHash` command.

Answer: `57492d33b7c0755bb411b22d2dfdfdf088cbbfcd010e30dd8d425d5fe66adff4`

### Question 7

The attacker managed to masquerade the real filename. Can you find it having the hash in your arsenal? 

We can look at the file hash with VirusTotal.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/7.7.png?raw=true)

Answer: `psexec.exe`

## Task 7

### Question 1

Can you identify the product name of the machine?

Go to `System Information`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/7.1.png?raw=true)

Answer: `Windows 7 Home Basic`

### Question 2

Can you find the name of the note left on the Desktop for the "Charles"?

Answer: `_R_E_A_D___T_H_I_S___AJYG1O_.txt`

### Question 3

Find the Windows Defender service; what is the name of its service DLL?

Answer: `MpSvc.dll`

### Question 4

The user manually downloaded a zip file from the web. Can you find the filename?

Answer: `eb5489216d4361f9e3650e6a6332f7ee21b0bc9f3f3a4018c69733949be1d481.zip`

### Question 5

Provide the filename of the malicious executable that got dropped on the user's Desktop.

Answer: `Endermanch@Cerber5.exe`

### Question 6

Provide the MD5 hash for the dropped malicious executable.

Answer: `fe1bc60a95b2c2d77cd5d232296a7fa4`

### Question 7

What is the name of the ransomware?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/redline/7.7.png?raw=true)

Answer: `Cerber`

## Task 8

### Question 1

Read the above.

Answer: `No answer needed`