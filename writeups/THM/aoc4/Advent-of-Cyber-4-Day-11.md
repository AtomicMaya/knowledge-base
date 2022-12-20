# Advent of Cyber 4 - Day 11

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the Windows version number that the memory image captured?

We run `python3 vol.py -f workstation.vmem windows.info`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day11/1.png?raw=true)

Answer: `10`

### Question 2

> What is the name of the binary/gift that secret Santa left?

We run `python3 vol.py -f workstation.vmem windows.pslist`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day11/2.png?raw=true)

Answer: `mysterygift.exe`

### Question 3

> What is the Process ID (PID) of this binary?

We check the associated column.

Answer: `2040`

### Question 4

> Dump the contents of this binary. How many files are dumped?

We run `python3 vol.py -f workstation.vmem windows.dumpfiles --pid 2040` and then count the number of results.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day11/4.png?raw=true)

Answer: `16`
