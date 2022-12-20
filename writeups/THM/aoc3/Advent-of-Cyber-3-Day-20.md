# Advent of Cyber - Day 20

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Open the terminal and navigate to the file on the desktop named 'testfile'. Using the 'strings' command, check the strings in the file. There is only a single line of output to the 'strings' command. What is the output?

Command: `strings testfile`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day20/1.png?raw=true)

Answer: `X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*`

### Question 2

Check the file type of 'testfile' using the 'file' command. What is the file type?

Command: `file testfile`

Answer: `EICAR virus test files`

### Question 3

Calculate the file's hash and search for it on VirusTotal. When was the file first seen in the wild?

Command: `sha256sum testfile`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day20/3.png?raw=true)

Answer: `2005-10-17 22:03:48`

### Question 4

On VirusTotal's detection tab, what is the classification assigned to the file by Microsoft?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day20/4.png?raw=true)

Answer: `Virus:DOS/EICAR_Test_File`

### Question 5

Go to [this link](https://www.eicar.org/?page_id=3950) to learn more about this file and what it is used for. What were the first two names of this file?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day20/5.png?raw=true)

Answer: `ducklin.htm or ducklin-html.htm`

### Question 6

The file has 68 characters in the start known as the known string. It can be appended with whitespace characters upto a limited number of characters. What is the maximum number of total characters that can be in the file?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day20/6.png?raw=true)

Answer: `128`
