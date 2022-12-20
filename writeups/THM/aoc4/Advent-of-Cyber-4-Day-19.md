# Advent of Cyber 4 - Day 19

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What device can be used to probe the signals being sent on electrical wires between two devices?

Answer: `Logic Analyser`

### Question 2

> USART is faster than SPI for communication? (Yea,Nay)

Answer: `Nay`

### Question 3

> USART communication uses fewer wires than SPI? (Yea,Nay)

Answer: `Yea`

### Question 4

> USART is faster than I2C for communication? (Yea,Nay)

Answer: `Nay`

### Question 5

> I2C uses more wires than SPI for communication? (Yea,Nay)

Answer: `Nay`

### Question 6

> SPI is faster than I2C for communication? (Yea,Nay)

Answer: `Yea`

### Question 7

> What is the maximum number of devices that can be connected on a single pair of I2C lines?

Answer: `1008`

### Question 8

> What is the new baud rate that is negotiated between the microprocessor and ESP32 chip?

Answer: `9600`

### Question 9

> What is the flag that is transmitted once the new baud rate was accepted?

By analyzing Channel 1, we obtain the following baud rate:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day19/9.1.png?raw=true)

By adding Channel 0, we get the response:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day19/9.2.png?raw=true)

When switching the Async Serial Analyzer to `9600bd` we get the following decoded message:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day19/9.3.png?raw=true)

Answer: `THM{Hacking.Hardware.Is.Fun}`