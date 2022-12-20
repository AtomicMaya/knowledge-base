# Advent of Cyber - Day 13

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Complete the username: p.....

Command: `net users`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/1.png?raw=true)

Answer: `pepper`

### Question 2

What is the OS version?

Command: `systeminfo | findstr /B /C:"OS Name" /C:"OS Version"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/2.png?raw=true)

Answer: `10.0.17763 N/A Build 17763`

### Question 3

What backup service did you find running on the system?

Command: `wmic service list | Out-File -FilePath dump.txt`

Here I am dumping it into a file for convenience's sake, but probably avoid doing this during an engagement.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/3.png?raw=true)

Answer: `IperiusSvc`

### Question 4

What is the path of the executable for the backup service you have identified?

Answer: `C:\Program Files (x86)\Iperius Backup\IperiusService.exe`

### Question 5

Run the whoami command on the connection you have received on your attacking machine. What user do you have?

Step 1:

Get `evil.bat` created.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.1.png?raw=true)

Step 2:

Create the backup job.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.2.png?raw=true)

Step 3:

Set the destination.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.3.png?raw=true)

Step 4:

Set up the pre-script.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.4.png?raw=true)

Step 5:

Start the listener: `nc -lvnp 1234`

Step 6:

Start the backup as a service:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.5.png?raw=true)

Step 7:

Profit!

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/5.6.png?raw=true)

Answer: `the-grinch-hack\thegrinch`

### Question 6

What is the content of the flag.txt file?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/6.png?raw=true)

Answer: `THM-736635221`

### Question 7

The Grinch forgot to delete a file where he kept notes about his schedule! Where can we find him at 5:30?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day13/7.png?raw=true)

Answer: `jazzercize`