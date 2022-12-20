# Advent of Cyber 4 - Day 10

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the Guard's flag?

First we prompt the guard.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.1.png?raw=true)

We then search any register that was equal to the number provided.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.2.png?raw=true)

Once we have the register we bookmark it.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.3.png?raw=true)

We re-prompt the guard, check the value in the register, throw as-is in python, and it spits out the decimal version.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.4.png?raw=true)

We enter this version:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.5.png?raw=true)

The guard lets us through.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.6.png?raw=true)

We interact again to obtain the flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/1.7.png?raw=true)

Answer: `THM{5_star_Fl4gzzz}`

### Question 2

> What is the Yeti's flag?

This time around we just look at decreasing registers.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/2.1.png?raw=true)

Once we iterate, we have an arbitrarily small amount of registers.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/2.2.png?raw=true)

We freeze it at 100.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/2.3.png?raw=true)

We survive.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/2.4.png?raw=true)

The Yeti gives us the flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day10/2.5.png?raw=true)

Answer: `THM{yetiyetiyetiflagflagflag}`