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
