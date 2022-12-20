# Splunk 2

For this box I used the browser based attack box for tasks 3 and 4, and later my Kali VM for tasks 5 and 6.

Link: [Splunk 2 Room on TryHackMe](https://tryhackme.com/room/splunk2gcd5)

## Task 1

### Question 1

Deployed the virtual machine and connected to the website found at $ip:8000

Answer: `No answer needed`

## Task 2

### Question 1

I'm ready to get hunting with Splunk.

Answer: `No answer needed`

## Task 3

### Question 1

Amber Turing was hoping for Frothly to be acquired by a potential competitor which fell through, but visited their website to find contact information for their executive team. What is the website domain that she visited?

By following along the instructions we use the command `index="botsv2" amber` to get some information about Amber.

With `index="botsv2" sourcetype="pan:traffic" amber` we can find the following IP address: `10.0.2.101`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.1-1.png?raw=true)

To look for HTTP connections including that IP, we use `index="botsv2" sourcetype="stream:http" 10.0.2.101`.

This yields 2147 events, but we can whittle it down.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.1-2.png?raw=true)

We can attempt to remove duplicate sites visited by using the `dedup` command, like so: `index="botsv2" sourcetype="stream:http" 10.0.2.101 | dedup site`

This brings the number of results down to 107.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.1-3.png?raw=true)

We can restrict the view to a table of the site column using: `index="botsv2" sourcetype="stream:http" 10.0.2.101 | dedup site | table site`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.1-4.png?raw=true)

Finally, a competitor is in the same industry, so we can add that as a search keyword:

`index="botsv2" sourcetype="stream:http" 10.0.2.101 *beer* | dedup site | table site`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.1-5.png?raw=true)

Answer: `www.berkbeer.com`

### Question 2

Amber found the executive contact information and sent him an email. What image file displayed the executive's contact information? Answer example: /path/image.ext

By using the `index="botsv2" sourcetype="stream:http" 10.0.2.101 www.berkbeer.com` query, we can find a few datapoints:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.2-1.png?raw=true)

We can further filter it to just the image collected by piping it through to the `table uri_path` command:

`index="botsv2" sourcetype="stream:http" 10.0.2.101 www.berkbeer.com | table uri_path`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.2-2.png?raw=true)

The two images that could be the correct answer are `/images/ceoberk.png` and `/images/chiefscience.png`. Chief Science Officers are rarely involved in such dealings so I went with the former.

Answer: `/images/ceoberk.png`

### Question 3

What is the CEO's name? Provide the first and last name.

To start, we need Amber's email address. 

The command `index="botsv2" sourcetype="stream:smtp" amber` produces the address `aturing@froth.ly`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.3-1.png?raw=true)

We can then use the command `index="botsv2" sourcetype="stream:smtp" aturing@froth.ly berkbeer.com | table _raw` to get 4 results (in raw format).

A text search for "berk" will reveal an "mberk@berkbeer.com", a search for that will reveal a "Martin Berk".

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.3-2.png?raw=true)

Answer: `Martin Berk`

### Question 4

What is the CEO's email address?

Answer: `mberk@berkbeer.com`

### Question 5

After the initial contact with the CEO, Amber contacted another employee at this competitor. What is that employee's email address?

By going back to our initial emails view and scrolling down, we find:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.5.png?raw=true)

Answer: `hbernhard@berkbeer.com`

### Question 6

What is the name of the file attachment that Amber sent to a contact at the competitor?

From the previous view, we can expand the attach_filename array to show the name of the filename.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.6.png?raw=true)

Answer: `Saccharomyces_cerevisiae_patent.docx`

### Question 7

What is Amber's personal email address?

By working off of the hint prompting us to look for encoded content, I found this base64 encoded block of text:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.7-1.png?raw=true)

I put that block into [Cyberchef](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)) to get the following:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/3.7-2.png?raw=true)

Answer: `ambersthebest@yeastiebeastie.com`

## Task 4

### Question 1

What version of TOR Browser did Amber install to obfuscate her web browsing? Answer guidance: Numeric with one or more delimiter.

The suggested searchstring is `index="botsv2" amber tor`, which yields hundreds of results. When attempting to download Tor Myself, the installer filename on Windows is `torbrowser-install`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.1-1.png?raw=true)

Searching for `index="botsv2" amber tor torbrowser-install` yields the following:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.1-2.png?raw=true)

Answer: `7.0.4`

### Question 2

What is the public IPv4 address of the server running www.brewertalk.com?

By searching for `index="botsv2" sourcetype="stream:http" www.brewertalk.com` and scrolling a bit, we find:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.2.png?raw=true)

Answer: `52.42.208.228`

### Question 3

Provide the IP address of the system used to run a web vulnerability scan against www.brewertalk.com.

By focusing on the day with the most events, we can investigate the most common src for all events involving the website.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.3.png?raw=true)

Answer: `45.77.65.211`

### Question 4

The IP address from Q#2 is also being used by a likely different piece of software to attack a URI path. What is the URI path? Answer guidance: Include the leading forward slash in your answer. Do not include the query string or other parts of the URI. Answer example: /phpinfo.php

By looking at this command `index="botsv2" sourcetype="stream:http" 52.42.208.228 | dedup uri_path` we can deduce that a number of filetypes exist (.css, .php, .js, etc.), but that this is likely a PHP backend. As such we expand our query `index="botsv2" sourcetype="stream:http" 52.42.208.228 php | dedup uri_path`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.4.png?raw=true)

Answer: `/member.php`

### Question 5

What SQL function is being abused on the URI path from the previous question?

When looking at the responses from before, we can filter using this query: `index="botsv2" sourcetype="stream:http" uri_path="/member.php"`

If we look a bit further, we can see the word: `error`, we can see the `updatexml` function is called and producess a XPath syntax error.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.5.png?raw=true)

Answer: `updatexml`

### Question 6

What was the value of the cookie that Kevin's browser transmitted to the malicious URL as part of an XSS attack? Answer guidance: All digits. Not the cookie name or symbols like an equal sign.

By filtering again using the command `index="botsv2" sourcetype="stream:http" 52.42.208.228 uri_path="/member.php"`, we can look at the `set_cookie` array. 

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.6.png?raw=true)

There are two different values: `1502408194` and `1502408189`, although only the latter works.

Answer: `1502408189`

### Question 7

What brewertalk.com username was maliciously created by a spear phishing attack?

By searching for `index="botsv2" sourcetype="stream:http" kevin`, we can find 13 events, in the first, within the `form_data` field, we can see the homograph `kIagerfield` be used to log into an account.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/4.7.png?raw=true)

Answer: `kIagerfield`

## Task 5

### Question 1

Mallory's critical PowerPoint presentation on her MacBook gets encrypted by ransomware on August 18. What is the name of this file after it was encrypted?

First, we look for devices that Mallory may own, so we perform the following search: `index="botsv2" mallory`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.1-1.png?raw=true)

This produces a ton of results, but also gives us `MACLORY-AIR13`, which corresponds to a MacBook Air, and is a fun pun on the name Mallory. Moving on.

We can then look for PowerPoint files (which used to end in `.ppt` and now usually end in `.pptx`) on this host.

The command for that would be `index="botsv2" host="MACLORY-AIR13" (*.ppt OR *.pptx)`

Note: Whilst many strings are not considered case sensitive in Splunk, `OR` definitely is.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.1-2.png?raw=true)

Answer: `Frothly_marketing_campaign_Q317.pptx.crypt`

### Question 2

There is a Games of Thrones movie file that was encrypted as well. What season and episode is it? 

For this question we can look at any file that would end with the `.crypt` extension with the `index="botsv2" host="MACLORY-AIR13" (*.crypt)` search query.

This however yields an unsightly 1103 events to filter out.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.2-1.png?raw=true)

We can further filter this by searching for `file_events` (because an encryption usually affects a file in some way, shape or form) using the following query: `index="botsv2" host="MACLORY-AIR13" (*.crypt) name="file_events"`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.2-2.png?raw=true)

This yields `S7E2`, which in standard series notation is `S07E02`.

Answer: `S07E02`

### Question 3

Kevin Lagerfield used a USB drive to move malware onto kutekitten, Mallory's personal MacBook. She ran the malware, which obfuscates itself during execution. Provide the vendor name of the USB drive Kevin likely used. Answer Guidance: Use time correlation to identify the USB drive.

`index="botsv2" host="kutekitten" name="file_events"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-1.png?raw=true)

This leads us to this suspicious filename: `Users/mkraeusen/Downloads/Important_HR_INFO_for_mkraeusen`

Looking for it with this query: `index="botsv2" host="kutekitten" \\/Users\\/mkraeusen\\/Downloads\\/Important_HR_INFO_for_mkraeusen` leads us to 


![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-2.png?raw=true)

produces the following hash: `befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271`, which [VirusTotal](https://www.virustotal.com/gui/file/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271) flags as malicious, leading us to think we are on the right path.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-3.png?raw=true)

Searching for `index="botsv2" host="kutekitten" usb` between `Thu Aug 03 17:19:07 2017 UTC` and `Thu Aug 03 19:19:07 2017 UTC` produces a manageable 52 events, which we can filter down to 30 using the `sourcetype="osquery_results"` filter.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-4.png?raw=true)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-5.png?raw=true)

Which leads us to find a `vendor_id` of `058f`, which if we plug into [the sz](https://the-sz.com/products/usbid/index.php?v=0x058f&p=&n=) leads us to `Alcor Micro Corp.`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.3-6.png?raw=true)

Answer: `Alcor Micro Corp.`

### Question 4

What programming language is at least part of the malware from the question above written in?

From the VirusTotal page mentioned above, we can see that it is `Perl`.

Answer: `Perl`

### Question 5

When was this malware first seen in the wild? Answer Guidance: YYYY-MM-DD

From VirusTotal, we can see that the name of the malware is called `FruitFly` (alternatively `Quimitchin`), and searching for that will lead us to [this MalwareBytes article](https://blog.malwarebytes.com/threat-analysis/2017/01/new-mac-backdoor-using-antiquated-code/), which was posted on 2017-01-18.

It isn't indicated (read: guessing backwards) when the malware was discovered, but it happened the day before.

Answer: `2017-01-17`

### Question 6

The malware infecting kutekitten uses dynamic DNS destinations to communicate with two C&C servers shortly after installation. What is the fully-qualified domain name (FQDN) of the first (alphabetically) of these destinations?

By plugging the hash from earlier (`befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271`) into [Hybrid Analysis](https://www.hybrid-analysis.com/sample/befa9bfe488244c64db096522b4fad73fc01ea8c4cd0323f1cbdee81ba008271), we get the following domains contacted:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/5.6.png?raw=true)

Answer: `eidk.duckdns.org`

### Question 7

From the question above, what is the fully-qualified domain name (FQDN) of the second (alphabetically) contacted C&C server?

Answer: `eidk.hopto.org`

## Task 6

### Question 1

A Federal law enforcement agency reports that Taedonggang often spear phishes its victims with zip files that have to be opened with a password. What is the name of the attachment sent to Frothly by a malicious Taedonggang actor?

We can run this query to find the name of the file.

`index="botsv2" sourcetype="stream:smtp" *.zip`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.1.png?raw=true)

Answer: `invoice.zip`

### Question 2

What is the password to open the zip file?

We just read through the message's content to find the password to the zip.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.2.png?raw=true)

Answer: `912345678`

### Question 3

The Taedonggang APT group encrypts most of their traffic with SSL. What is the "SSL Issuer" that they use for the majority of their traffic? Answer guidance: Copy the field exactly, including spaces.

First, copy all of the base64 representation of the file to a text file (in my case `~/zip.b64`).

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-1.png?raw=true)

Then, we write a bit of Python: 

```py
f = open("zip.b64")
d = f.readlines()
f.close()

d = [a.replace("\n", "").replace(" ", "").replace("\t", "") for a in d]

out = "".join(d)
f2 = open("zip.b64.concat", "w")
f2.write(out)
f2.close()
```

This should produce a file named `zip.b64.concat` which looks like this:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-2.png?raw=true)

And then we can use the command line to produce a zip, unzip it, then get the hash for the file within!

```bash
cat zip.b64.concat | base64 --decode > invoice.zip
unzip invoice.zip
sha256sum invoice.doc
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-3.png?raw=true)

By plugging the hash from the file (`d8834aaa5ad6d8ee5ae71e042aca5cab960e73a6827e45339620359633608cf1`) into [Hybrid Analysis](https://www.hybrid-analysis.com/sample/d8834aaa5ad6d8ee5ae71e042aca5cab960e73a6827e45339620359633608cf1), we get the following domains contacted:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-4.png?raw=true)
![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-5.png?raw=true)

Weirdly enough, address number 2 (`45.77.65.211`) is the same as for question 4.3.

If we search for it in Splunk, we get the following: 

`index="botsv2" sourcetype="stream:tcp" "45.77.65.211"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.3-6.png?raw=true)

Answer: `C = US`

### Question 4

What unusual file (for an American company) does winsys32.dll cause to be downloaded into the Frothly environment?

We can first look at `index="botsv2" winsys32.dll`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.4-1.png?raw=true)

It gets loaded by `ftp.exe`, so maybe we can look at FTP streams: `index="botsv2" sourcetype="stream:ftp"`

To filter it out a bit, we can limit ourselves to FTP downloads, which are the RETR method.

`index="botsv2" sourcetype="stream:ftp" method=RETR`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.4-2.png?raw=true)

We can see it download a weird `.hwp` file, the name of which is the answer.

Answer: `나는_데이비드를_사랑한다.hwp`

### Question 5

What is the first and last name of the poor innocent sap who was implicated in the metadata of the file that executed PowerShell Empire on the first victim's workstation? Answer example: John Smith

If we look at the file `invoice.doc` with the `file` utility, we get some interesting information, including the name of the Author.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.5.png?raw=true)

Answer: `Ryan Kovar`

### Question 6

Within the document, what kind of points is mentioned if you found the text?

If you were to open AnyRun link provided in the description, you would see the text mentioned.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.6.png?raw=true)

Answer: `CyberEastEgg`

### Question 7

To maintain persistence in the Frothly network, Taedonggang APT configured several Scheduled Tasks to beacon back to their C2 server. What single webpage is most contacted by these Scheduled Tasks? Answer example: index.php or images.html

Scheduled tasks are usually set up featuring some call to `schtasks.exe`, soo we can look at references to it in Splunk.

`index="botsv2" schtasks.exe`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.7-1.png?raw=true)

This produces two types of logs: Windows Events and Sysmon Logs.

Let us filter on the latter: `index="botsv2" sourcetype="xmlwineventlog:microsoft-windows-sysmon/operational" schtasks.exe`

If we focus around the day of the incident, we should see a Powershell command be executed:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.7-2.png?raw=true)

Within the fields is `CommandLine` which references the registry key `HKLM:\Software\Microsoft\Network debug`, which we can then query for:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.7-3.png?raw=true)

`index="botsv2" source="winregistry" "Software\\Microsoft\\Network"`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.7-4.png?raw=true)

This produces some base64 code, which we can plug into CyberChef (the weird dots can be removed with the `Remove Null Bytes` element).

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/splunk2/6.7-5.png?raw=true)

This references one single php file (`process.php`) and since this event is from the same timeframe as the rest of the incident, we assume it is the correct file.

Answer: `process.php`

## Task 7

### Question 1

You leveled up your Splunk-fu thanks to the BOTSv2 dataset.

Answer: `No answer needed`