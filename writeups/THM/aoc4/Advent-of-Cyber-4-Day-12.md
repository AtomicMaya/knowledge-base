# Advent of Cyber 4 - Day 12

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the architecture of the malware sample? (32-bit/64-bit)

We look at the architecture section in DIE.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/1.png?raw=true)

Answer: `64-bit`

### Question 2

> What is the packer used in the malware sample? (format: lowercase)

The packer is written in the DIE scan results.

Answer: `upx`

### Question 3

> What is the compiler used to build the malware sample? (format: lowercase)

After decompiling the sample with `upx -d mysterygift` we can process it with `capa mysterygift` and find the compiler name.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/3.png?raw=true)

Answer: `nim`

### Question 4

> How many MITRE ATT&CK techniques have been discovered attributed to the DISCOVERY tactic?

In the ATT&CK Tactic section we can see two Techniques.

Answer: `2`

### Question 5

> What is the registry key abused by the malware?

We check for one of the first `RegCloseKey` operations in ProcMon.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/5.png?raw=true)

Answer: `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

### Question 6

> What is the value written on the registry key based on the previous question?

We check for the next `RegSetValue` operation in ProcMon.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/6.png?raw=true)

Answer: `C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\wishes.bat`

### Question 7

> What are the names of two files created by the malware under the C:\Users\Administrator\ directory? (format: file1,file2 in alphabetical order)

We find `CreateFile` operations in ProcMon.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/7.png?raw=true)

Answer: `test.jpg,wishes.bat`

### Question 8

> What are the two domains wherein malware has initiated a network connection? (format: domain1,domain2 in alphabetical order)

We look for the two `TCP Connect` operations in ProcMon.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/8.png?raw=true)

Answer: `bestfestivalcompany.thm,virustotal.com`

### Question 9

> Going back to strings inside the malware sample, what is the complete URL used to download the file hosted in the first domain accessed by the malware?

In DIE we filter on `http` strings and find the correct string:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day12/9.png?raw=true)

Answer: `http://bestfestivalcompany.thm/favicon.ico`
