# Advent of Cyber - Day 10

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Help McSkidy and run `nmap -sT MACHINE_IP`. How many ports are open between 1 and 100?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/1.png?raw=true)

Answer: `2`

### Question 2

What is the smallest port number that is open?

Answer: `22`

### Question 3

What is the service related to the highest port number you found in the first question?

Answer: `http`

### Question 4

Now run `nmap -sS MACHINE_IP`. Did you get the same results? (Y/N)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/4.png?raw=true)

Answer: `Y`

### Question 5

If you want Nmap to detect the version info of the services installed, you can use `nmap -sV MACHINE_IP`. What is the version number of the web server?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/5.png?raw=true)

Answer: `Apache httpd 2.4.4`

### Question 6

By checking the vulnerabilities related to the installed web server, you learn that there is a critical vulnerability that allows path traversal and remote code execution. Now you can tell McSkidy that Grinch Enterprises used this vulnerability. What is the CVE number of the vulnerability that was solved in version 2.4.51?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/6.png?raw=true)

Answer: `CVE-2021-42013`

### Question 7

You are putting the pieces together and have a good idea of how your web server was exploited. McSkidy is suspicious that the attacker might have installed a backdoor. She asks you to check if there is some service listening on an uncommon port, i.e. outside the 1000 common ports that Nmap scans by default. She explains that adding -p1-65535 or -p- will scan all 65,535 TCP ports instead of only scanning the 1000 most common ports. What is the port number that appeared in the results now?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/7.png?raw=true)

Answer: `20212`

### Question 8

What is the name of the program listening on the newly discovered port?

Command: `nmap -sV 10.10.185.85 -p 20212 -T4 -vv`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day10/8.png?raw=true)

Answer: `telnetd`

### Question 9

If you would like to learn more about the topics covered in today’s tasks, we recommend checking out the Network Security module.

Answer: `No answer needed`