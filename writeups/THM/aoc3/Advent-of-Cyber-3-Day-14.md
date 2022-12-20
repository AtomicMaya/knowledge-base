# Advent of Cyber - Day 14

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

How many pages did the dirb scan find with its default wordlist?

Command: `gobuster dir --url $ip -w /usr/share/wordlists/dirb/common.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/1.png?raw=true)

Answer: `4`

### Question 2

How many scripts do you see in the /home/thegrinch/scripts folder?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/2.png?raw=true)

Answer: `4`

### Question 3

What are the five characters following $6$G in pepper's password hash?

Command: `nano /home/thegrinch/scripts/loot.sh`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/3.1.png?raw=true)

Then we refresh the browser page at `http://$ip/admin`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/3.2.png?raw=true)

Answer: `ZUP42`

### Question 4

What is the content of the flag.txt file on the Grinch's user’s desktop?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/4.1.png?raw=true)

Then we refresh the browser page at `http://$ip/admin`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day14/4.2.png?raw=true)

Answer: `DI3H4rdIsTheBestX-masMovie!`