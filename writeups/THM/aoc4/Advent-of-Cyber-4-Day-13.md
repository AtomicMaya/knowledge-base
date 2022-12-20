# Advent of Cyber 4 - Day 13

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> View the "Protocol Hierarchy" menu. What is the "Percent Packets" value of the "Hypertext Transfer Protocol"?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/1.png?raw=true)

Answer: `0.3`

### Question 2

> View the "Conversations". Navigate to the TCP section. Which port number has received more than 1000 packets?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/2.png?raw=true)

Answer: `3389`

### Question 3

> What is the service name of the used protocol that received more than 1000 packets?

Answer: `RDP`

### Question 4

> Filter the DNS packets. What are the domain names? Enter the domains in alphabetical order and defanged format. (format: `domain[.]zzz,domain[.]zzz`)

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/4.png?raw=true)

Answer: `bestfestivalcompany[.]thm,cdn[.]bandityeti[.]thm`

### Question 5

> Filter the HTTP packets. What are the names of the requested files? Enter the names in alphabetical order and in defanged format. (format: `file[.]xyz,file[.]xyz`)

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/5.png?raw=true)

Answer: `favicon[.]ico,mysterygift[.]exe`

### Question 6

> Which IP address downloaded the executable file? Enter your answer in defanged format.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/6.png?raw=true)

Answer: `10[.]10[.]29[.]186`

### Question 7

> Which domain address hosts the malicious file? Enter your answer in defanged format.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/7.png?raw=true)

Answer: `cdn[.]bandityeti[.]thm`

### Question 8

> What is the "user-agent" value used to download the non-executable file?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/8.png?raw=true)

Answer: `Nim httpclient/1.6.8`

### Question 9

> Export objects from the PCAP file. Calculate the file hashes. What is the sha256 hash value of the executable file?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/9.png?raw=true)

Answer: `0ce160a54d10f8e81448d0360af5c2948ff6a4dbb493fe4be756fc3e2c3f900f`

### Question 10

> Search the hash value of the executable file on VirusTotal. Navigate to the "Behaviour" section. There are multiple IP addresses associated with this file.

> What are the connected IP addresses? Enter the IP addressed defanged and in numerical order. (format: IPADDR,IPADDR)

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/10.1.png?raw=true)

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day13/10.2.png?raw=true)

Answer: `20[.]99[.]133[.]109,20[.]99[.]184[.]37,23[.]216[.]147[.]64,23[.]216[.]147[.]76`
