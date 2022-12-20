# Disk Analysis & Autopsy

For this box I used Remmina whilst on Kali.

Link: [Disk Analysis & Autopsy on TryHackMe](https://tryhackme.com/room/autopsy2ze0)

## Task 1

Start Autopsy, then load the case file (`C:\Users\Administrator\Desktop\Case Files\Tryhackme.aut`), then load up the associated file (`C:\Users\Administrator\Desktop\Case Files\HASAN2.E01`)

### Question 1

What is the MD5 hash of the E01 image?

To locate the MD5 hash, go to the `Data Sources` tab, right-click on `HASAN2.E01`, click on `View Summary Information`, then go to the `Container` tab in the newly opened window, you should find the hash.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/1.png?raw=true)

Answer: `3f08c518adb3b5c1359849657a9b2079`

### Question 2

What is the computer account name?

Go to the `Operating System Information` tab and you'll be able to find the name of the `SYSTEM` source file.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/2.png?raw=true)

Answer: `DESKTOP-0R59DJ3`

### Question 3

List all the user accounts. (alphabetical order)

Go to the `Operating System User Account` tab and you'll be able to find the name of the user accounts.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/3.png?raw=true)

Answer: `H4S4N, joshwa, keshav, sandhya, shreya, sivapriya, srini, suba`

### Question 4

Who was the last user to log into the computer?

Sort the previous table by `Date Accessed`

Answer: `sivapriya`

### Question 5

What was the IP address of the computer?

This one took me a while, but if you look at the Data Source (`Data Sources/vol3/`) in a specific folder: `Program Files (x86)/Look@Lan`, there is a file called `irunin.ini` which has a line called `%LANIP%`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/5.png?raw=true)

Answer: `192.168.130.216`

### Question 6

What was the MAC address of the computer? (XX-XX-XX-XX-XX-XX)

The line under the IP address is a MAC address that is just not in the expected format.

Answer: `08-00-27-2c-c4-b9`

### Question 7

Name the network cards on this computer.

A "quick" keyword search for the term `Ethernet` produces a lot of results, but by digging a little, we can find some Diagnostics logs.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/7.png?raw=true)

Answer: `Intel(R) PRO/1000 MT Desktop Adapter`

### Question 8

What is the name of the network monitoring tool?

From our finding of the IP address, we have the name of the tool.

Answer: `Look@LAN`

### Question 9

A user bookmarked a Google Maps location. What are the coordinates of the location?

If we go to the `Web bookmarks` tab, we can find one that is for a `google.com/maps` URL.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/9.png?raw=true)

Answer: `12°52'23.0" 80°13'25.0"`

### Question 10

A user has his full name printed on his desktop wallpaper. What is the user's full name?

We need to go to the "Image/Vide Gallery", and then go through the Users folder to look for images there. Thankfully there are very few and we can just export them and look at them with Paint or something.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/10.png?raw=true)

Answer: `Anto Joshwa`

### Question 11

A user had a file on her desktop. It had a flag but she changed the flag using PowerShell. What was the first flag?

We are told the flag was changed using PowerShell, so we can look for PowerShell history, which a convenient Google Search tells us to be `%userprofile%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadline\ConsoleHost_history.txt`.

We can look for this file in each folder, or we can just search for it using Autopsy:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/11.png?raw=true)

Answer: `flag{HarleyQuinnForQueen}` 

### Question 12

The same user found an exploit to escalate privileges on the computer. What was the message to the device owner?

In the same file as earlier, we saw the text "I hacked you" being added to a file called `Desktop/lala.txt`

This flag got rejected, but that is due to the format not being specified.

Answer: `flag{I-hacked-you}`

### Question 13

2 hack tools focused on passwords were found in the system. What are the names of these tools? (alphabetical order)

We can take a look around for detection/anti-virus software, and see that Windows Defender exists. 

Windows Defender stores its logs in `ProgramData/Microsoft/Windows Defender` (and stores detections in the `Scans/History/Service/DetectionHistory` subfolder) (Google FTW once more).

Look through the files.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/13-1.png?raw=true)
![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/13-2.png?raw=true)

Answer: `LaZagne, Mimikatz`

### Question 14

There is a YARA file on the computer. Inspect the file. What is the name of the author?

If we search for `.yar` we find a reference to a file named `kiwi_passwords.yar`.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/14.png?raw=true)

If we google that filename, we land on [this file](https://github.com/mikesxrs/Open-Source-YARA-rules/blob/master/mimikatz/kiwi_passwords.yar) on GitHub.

There is the name of the author: "Benjamin DELPY `gentilkiwi`"

(This is however not the flag, you need to replace the backticks with parentheses).

Answer: `Benjamin DELPY (gentilkiwi)`

### Question 15

One of the users wanted to exploit a domain controller with an MS-NRPC based exploit. What is the filename of the archive that you found? (include the spaces in your answer) 

If we look in the `Recent Documents`, we can find a `.zip` file with the name of a type of security system.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/da_autopsy/15.png?raw=true)

Answer: `2.2.0 20200918 Zerologon encrypted.zip`