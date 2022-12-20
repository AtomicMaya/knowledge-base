# Advent of Cyber 4 - Day 5

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> Use Hydra to find the VNC password of the target with IP address `$MACHINE_IP`. What is the password?

We run `nmap` in service discovery mode like so: `nmap -sS $IP` to check that VNC is running on the machine.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day5/1.1.png?raw=true)

We then run `hydra` to find the password for `mark`: `hydra -P /usr/share/wordlists/rockyou.txt $IP vnc`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day5/1.2.png?raw=true)

Answer: `1q2w3e4r`

### Question 2

> Using a VNC client on the AttackBox, connect to the target of IP address `MACHINE_IP`. What is the flag written on the target’s screen?

We use Remmina:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day5/2.1.png?raw=true)

We enter the password that we found before:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day5/2.2.png?raw=true)

We then find the password:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day5/2.3.png?raw=true)

Answer: `THM{I_SEE_YOUR_SCREEN}`