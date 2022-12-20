# Advent of Cyber 4 - Day 3

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the name of the Registrar for the domain santagift.shop?

We take a look using the ICANN Lookup website: [https://lookup.icann.org/en/lookup](https://lookup.icann.org/en/lookup)

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day3/1.png?raw=true)

Answer: `NAMECHEAP INC`

### Question 2

> Find the website's source code (repository) on [github.com](https://github.com/) and open the file containing sensitive credentials. Can you find the flag?

There it's just a matter of looking for the URL, and finding the oldest repository involved.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day3/2.1.png?raw=true)

There we look for interesting files, such as for example `config.php`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day3/2.2.png?raw=true)

This produces a flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day3/2.3.png?raw=true)

Answer: `{THM_OSINT_WORKS}`

### Question 3

> What is the name of the file containing passwords?

(See Q2)

Answer: `config.php`

### Question 4

> What is the name of the QA server associated with the website?

If we scroll down in the file a bit, we can see the following:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day3/4.png?raw=true)

Answer: `qa.santagift.shop`

### Question 5

> What is the DB_PASSWORD that is being reused between the QA and PROD environments?

(See Q4)

Answer: `S@nta2022`