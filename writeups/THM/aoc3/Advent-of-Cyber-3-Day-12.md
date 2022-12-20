# Advent of Cyber - Day 12

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Scan the target server with the IP MACHINE_IP. Remember that MS Windows hosts block pings by default, so we need to add -Pn, for example, nmap -Pn MACHINE_IP for the scan to work correctly. How many TCP ports are open?

Command: `nmap -Pn MACHINE_IP -T3`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day12/1.png?raw=true)

Answer: `7`

### Question 2

In the scan results you received earlier, you should be able to spot NFS or mountd, depending on whether you used the -sV option with Nmap or not. Which port is detected by Nmap as NFS or using the mountd service?

Answer: `2049`

### Question 3

How many shares did you find?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day12/3.png?raw=true)

Answer: `4`

### Question 4

How many shares show “everyone”?

Answer: `3`

### Question 5

What is the title of file 2680-0.txt?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day12/5.png?raw=true)

Answer: `Meditations`

### Question 6

It seems that Grinch Enterprises has forgotten their SSH keys on our system. One of the shares contains a private key used for SSH authentication (id_rsa). What is the name of the share?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day12/6.png?raw=true)

Answer: `confidential`

### Question 7

We can calculate the MD5 sum of a file using md5sum FILENAME. What is the MD5 sum of id_rsa?

Answer: `3e2d315a38f377f304f5598dc2f044de`