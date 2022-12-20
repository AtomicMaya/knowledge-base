# Advent of Cyber - Day 9

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

In the HTTP #1 - GET requests section, which directory is found on the web server?

By using the `http.request.method == GET` filter:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/1.png?raw=true)

Answer: `login`

### Question 2

What is the username and password used in the login page in the HTTP #2 - POST section? 

By using the `http.request.method == POST` filter:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/2.png?raw=true)

Answer: `McSkidy:Christmas2021!`

### Question 3

What is the User-Agent's name that has been sent in HTTP #2 - POST section?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/3.png?raw=true)

Answer: `TryHackMe-UserAgent-THM{d8ab1be969825f2c5c937aec23d55bc9}`

### Question 4

In the DNS section, there is a TXT DNS query. What is the flag in the message of that DNS query?

By using the `dns.txt` filter:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/4.png?raw=true)

Answer: `THM{dd63a80bf9fdd21aabbf70af7438c257}`

### Question 5

In the FTP section, what is the FTP login password?

By using the `ftp` filter:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/5.png?raw=true)

Answer: `TryH@ckM3!`

### Question 6

In the FTP section, what is the FTP command used to upload the secret.txt  file?

From the previous screenshot, we can see `STOR secret.txt`

Answer: `STOR`

### Question 7

In the FTP section, what is the content of the secret.txt file?

We need to change the filter to include `FTP Data`: `ftp or ftp-data` and look for the command following the `STOR` request:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day9/7.png?raw=true)

Answer: `123^-^321`
