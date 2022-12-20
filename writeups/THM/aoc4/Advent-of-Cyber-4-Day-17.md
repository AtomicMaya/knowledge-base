# Advent of Cyber 4 - Day 17

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> Filtering for Usernames: How many usernames fit the syntax above?

Command: `egrep '^[a-zA-Z0-9]{6-12}$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/1.png?raw=true)

Answer: `8`

### Question 2

> Filtering for Usernames: One username consists of a readable word concatenated with a number. What is it?

Answer: `User35`

### Question 3

> Filtering for Emails: How many emails fit the syntax above?

Command: `egrep '^.+@.+\.com$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/3.png?raw=true)

Answer: `11`

### Question 4

> Filtering for Emails: How many unique domains are there?

Answer: `8`

### Question 5

> Filtering for Emails: What is the domain of the email with the local-part "lewisham44"?

Command: `egrep '^lewisham44@.+\..+$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/5.png?raw=true)

Answer: `amg.com`

### Question 6

> Filtering for Emails: What is the domain of the email with the local-part "maxximax"?

Command: `egrep '^maxximax@.+\..+$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/6.png?raw=true)

Answer: `fedfull.com`

### Question 7

> Filtering for Emails: What is the local-part of the email with the domain name "hotmail.com"?

Command: `egrep '^.+@hotmail\.com$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/7.png?raw=true)

Answer: `hussain.volt`

### Question 8

> Filtering for URLs: How many URLs fit the syntax provided?

Command: `egrep '^http(s?):(www\.)?.+\..+$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/8.png?raw=true)

Answer: `16`

### Question 9

> Filtering for URLs: How many of these URLs start with "https"?

Command: `egrep '^https:(www\.)?.+\..+$' strings`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day17/9.png?raw=true)

Answer: `7`
