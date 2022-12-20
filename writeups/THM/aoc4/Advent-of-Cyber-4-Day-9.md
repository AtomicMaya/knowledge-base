# Advent of Cyber 4 - Day 9

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> Deploy the attached VM, and wait a few minutes. What ports are open?

Run `nmap -sV -sS $IP`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/1.png?raw=true)

Answer: `80`

### Question 2

> What framework is the web application developed with?

Browse to the page.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/2.png?raw=true)

Answer: `CVE-2021-3129`

### Question 3

> What CVE is the application vulnerable to?

We search for `laravel` and use the `info` term to get the details of the CVE.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/3.png?raw=true)

Answer: `CVE-2021-3129`

### Question 4

> What command can be used to upgrade the last opened session to a Meterpreter session?

From the explanation we find:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/6.png?raw=true)

Answer: `sessions -u -1`

### Question 5

> What file indicates a session has been opened within a Docker container?

From the internet: `/.dockerenv`

Answer: `/.dockerenv`

### Question 6

> What file often contains useful credentials for web applications?

See (Question 4)

Answer: `.env`

### Question 7

> What database table contains useful credentials?

We find the table schema dump, there is a table called `users`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/7.png?raw=true)

Answer: `users`

### Question 8

> What is Santa's password?

Answer: `p4$$w0rd`

### Question 9

> What ports are open on the host machine?

We run `proxychains -q nmap -n -sT -Pn -p 22,80,443,5432 172.17.0.1`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/9.png?raw=true)

Answer: `22,80`

### Question 10

> What is the root flag?

We login with the credentials and get the root flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day9/10.png?raw=true)

Answer: `THM{47C61A0FA8738BA77308A8A600F88E4B}`