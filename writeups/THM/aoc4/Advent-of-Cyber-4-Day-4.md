# Advent of Cyber 4 - Day 4

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the name of the HTTP server running on the remote host?

We run `nmap` in service discovery mode like so: `nmap -sV -sS $IP`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day4/1.png?raw=true)

Answer: `Apache`

### Question 2

> What is the name of the service running on port 22 on the QA server?

Answer: `ssh`

### Question 3

> What is the name of the service running on port 22 on the QA server?

We access the SMB share by accessing `smb://$IP` in our file explorer. There we see three shares, including `admins`. There we log in with the credentials provided in the challenge `ubuntu:S@nta2022`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day4/3.1.png?raw=true)

We find the `flag.txt` file:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day4/3.3.png?raw=true)

Answer: `{THM_SANTA_SMB_SERVER}`

### Question 4

> What is the password for the username santahr?

We look into the `userlist.txt` file and find the correct password:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day4/4.png?raw=true)

Answer: `santa25`