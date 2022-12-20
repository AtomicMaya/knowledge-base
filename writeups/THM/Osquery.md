# Osquery

For this box I used Remmina on Kali Linux while connected to the TryHackMe VPN.

Link: [Osquery Room on TryHackMe](https://tryhackme.com/room/osqueryf8)

## Task 1

### Question 1

Ready to learn Osquery!

Answer: `No answer needed`

## Task 2

### Question 1

Attached VM was started. Ready to proceed.

Answer: `No answer needed`

## Task 3

### Question 1

What is the Osquery version?

`osqueryi --version`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/3.1.png?raw=true)

Answer: `4.6.0.2`

### Question 2

What is the SQLite version?

In osquery, by using the `.summary`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/3.2.png?raw=true)

Answer: `3.34.0`

### Question 3

What is the default output mode?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/3.3.png?raw=true)

Answer: `pretty`

### Question 4

What is the meta-command to set the output to show one value per line?

Answer: `.mode line`

### Question 5

What are the 2 meta-commands to exit osquery?

Answer: `.exit, .quit`

## Task 4

I used the Osquery documentation accessible [here]() and set it to version 4.6.0.

### Question 1

What table would you query to get the version of Osquery installed on the Windows endpoint?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/4.1.png?raw=true)

Answer: `osquery_info`

### Question 2

How many tables are there for this version of Osquery?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/4.2.png?raw=true)

Answer: `266`

### Question 3

How many tables are there for this version of Osquery?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/4.3.png?raw=true)

Answer: `96`

### Question 4

How many tables are compatible with Linux?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/4.4.png?raw=true)

Answer: `155`

### Question 5

What is the first table listed that is compatible with both Linux and Windows?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/4.5.png?raw=true)

Answer: `arp_cache`

## Task 5

### Question 1

What is the query to show the username field from the users table where the username is 3 characters long and ends with 'en'? (use single quotes in your answer)

Answer: `select username from users where username like '_en';`

## Task 6

### Question 1

What is the Osquery Enroll Secret?

Navigate to the bottom of the `Admin, App Settings`

Answer: `k3hFh30bUrU7nAC3DmsCCyb1mT8HoDkt`

### Question 2

What is the Osquery version?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/6.2.png?raw=true)

### Question 3

What is the path for the running osqueryd.exe process?

Go to Task Manager, find the `osquery daemon and shell` process, select `Properties` and then copy the `Location` and append `osqueryd.exe`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/6.3-1.png?raw=true)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/6.3-2.png?raw=true)

Answer: `C:\Users\Administrator\Desktop\launcher\windows\osqueryd.exe`

## Task 7

### Question 1

According to the polylogyx readme, how many 'features' does the plug-in add to the Osquery core?

The current README shows 25, but the correct answer is 23 (looking at edits over time, also accessible by "guessing" backwards).

Answer: `23`

## Task 8

### Question 1

What is the 'current_value' for kernel.osrelease?

`select * from kernel_info;`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.1.png?raw=true)

Answer: `4.4.0-17763-Microsoft`

### Question 2

What is the uid for the bravo user?

`select username, uid from users where username = 'bravo';`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.2.png?raw=true)

Answer: `1002`

### Question 3

One of the users performed a 'Binary Padding' attack. What was the target file in the attack?

`select command from shell_history limit 12;` (I added the limit to cleanly wrap the image)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.3.png?raw=true)

Answer: `notsus`

### Question 4

What is the hash value for this file?

`md5sum notsus`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.4.png?raw=true)

Answer: `3df6a21c6d0c554719cffa6ee2ae0df7`

### Question 5

Check all file hashes in the home directory for each user. One file will not show any hashes. Which file is that?

`select * from hash where path='/home/tryhackme' and directory = '/home/tryhackme';`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.5.png?raw=true)

Answer: `fleet.zip`

### Question 6

There is a file that is categorized as malicious in one of the home directories. Query the Yara table to find this file. Use the sigfile which is saved in '/var/osquery/yara/scanner.yara'. Which file is it?

`yara /var/osquery/yara/scanner.yara /home/charlie`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.6-1.png?raw=true)

`select * from yara where path='/home/charlie/notes' and sigfile='/var/osquery/yara/scanner.yara';`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.6-2.png?raw=true)

Answer: `notes`

### Question 7

What were the 'matches'?

Answer: `eicar_av_test,eicar_substring_test`

### Question 8

Scan the file from Q#3 with the same Yara file. What is the entry for 'strings'?

`yara /var/osquery/yara/scanner.yara /home/tryhackme`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.8-1.png?raw=true)

`select * from yara where path='/home/tryhackme/notsus' and sigfile='/var/osquery/yara/scanner.yara';`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/8.8-2.png?raw=true)

Answer: `$eicar_substring:1b`

## Task 9

### Question 1

What is the description for the Windows Defender Service?

`select name, description from services where name like 'WinDef%';`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.1.png?raw=true)

Answer: `Helps protect users from malware and other potentially unwanted software`

### Question 2

There is another security agent on the Windows endpoint. What is the name of this agent?

`select name from programs;`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.2.png?raw=true)

Answer: `AlienVault Agent`

### Question 3

What is required with win_event_log_data?

From [the documentation](https://github.com/polylogyx/osq-ext-bin/blob/master/README.md) we gather that the `source` field is required.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.3.png?raw=true)

Answer: `source`

### Question 4

How many sources are returned for win_event_log_channels?

`select count(*) from win_event_log_channels;`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.4.png?raw=true)

Answer: `1076`

### Question 5

What is the schema for win_event_log_data?

From [the documentation](https://github.com/polylogyx/osq-ext-bin/blob/master/tables-schema/win_event_log_data.table), we can see the table schema.

From within Osquery, we can get the schema with the `.schema win_event_log_data`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.5.png?raw=true)

Answer: 
```
CREATE TABLE win_event_log_data(`time` BIGINT, `datetime` TEXT, `source` TEXT, `provider_name` TEXT, `provider_guid` TEXT, `eventid` INTEGER, `task` INTEGER, `level` INTEGER, `keywords` BIGINT, `data` TEXT, `eid` TEXT HIDDEN);`
```

### Question 6

The previous file scanned on the Linux endpoint with Yara is on the Windows endpoint.  What date/time was this file first detected? (Answer format: YYYY-MM-DD HH:MM:SS)

`select eventid, datetime from win_event_log_data where source='Microsoft-Windows-Windows Defender/Operational' and eventid=1116;`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.6.png?raw=true)

Answer: `2021-04-01 00:50:44`

### Question 7

What is the query to find the first Sysmon event? Select only the event id, order by date/time, and limit the output to only 1 entry.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/osquery/9.7.png?raw=true)

Answer: `select eventid FROM win_event_log_data where source='Microsoft-Windows-Sysmon/Operational' order by datetime asc limit 1;`

### Question 8

What is the Sysmon event id?

Answer: `16`

## Task 10

### Question 1

Leveled up with Osquery!

Answer: `No answer needed`