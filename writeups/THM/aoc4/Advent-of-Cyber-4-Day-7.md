# Advent of Cyber 4 - Day 7

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the version of CyberChef found in the attached VM?

We look at the website header.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day7/1.png?raw=true)

Answer: `9.49.0`

### Question 2

> How many recipes were used to extract URLs from the malicious doc?

There are 10 steps.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day7/2.png?raw=true)

Answer: `10`

### Question 3

> We found a URL that was downloading a suspicious file; what is the name of that malware?

Once more, we look at the `From:` header.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day7/3.png?raw=true)

Answer: `mysterygift.exe`

### Question 4

> What is the last defanged URL of the bandityeti domain found in the last step?

Answer: `hxxps[://]cdn[.]bandityeti[.]THM/files/index/`

### Question 5

> What is hidden in the value of the Message-ID field?

What is the ticket found in one of the domains? (Format: `Domain/<GOLDEN_FLAG>`)

Answer: `THM_MYSTERY_FLAG`