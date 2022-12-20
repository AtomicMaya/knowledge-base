# Advent of Cyber - Day 7

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Interact with the MongoDB server to find the flag. What is the flag?

Launch `mongo` in the terminal.

```mongo
show databases
use flagdb
db.getCollectionNames()
db.flagColl.find()
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day7/1.png?raw=true)

Answer: `THM{8814a5e6662a963f7df23ee59d944f9}`

### Question 2

We discussed how to bypass login pages as an admin. Can you log into the application that Grinch Enterprise controls as admin and retrieve the flag?

Use the knowledge given in AoC3 day 4 to setup and run Burp Suite proxy to intercept the HTTP request for the login page. Then modify the POST parameter.

First we open BurpSuite, activate the Proxy in Firefox, then visit the provided IP.

We then try to login and intercept the request and modify it to become `username=admin&password[$ne]=meep`, then forward it accordingly.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day7/2-1.png?raw=true)

We then visit the flag page to get the following.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day7/2-2.png?raw=true)

Answer: `THM{b6b304f5d5834a4d089b570840b467a8}`

### Question 3

Once you are logged in, use the gift search page to list all usernames that have `guest` roles. What is the flag?

We can start a request, which will put us at the endpoint `http://$ip/search?username=test&role=user`, which we can modify like so: `http://$ip/search?username[$ne]=meep&role=guest`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day7/3.png?raw=true)

Answer: `THM{2ec099f2d602cc4968c5267970be1326}`

### Question 4

Use the gift search page to perform NoSQL injection and retrieve the `mcskidy` record. What is the details record?

We can modify the previous request like so (assuming once more the keyword `meep` is not in use in production): `http://$ip/search?username=mcskidy&role[$ne]=meep`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day7/4.png?raw=true)

Answer: `ID:6184f516ef6da50433f100f4:mcskidy:admin`