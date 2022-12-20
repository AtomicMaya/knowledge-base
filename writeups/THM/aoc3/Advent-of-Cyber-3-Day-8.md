# Advent of Cyber - Day 8

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

If you want to RDP into the machine, start the AttackBox and enter the following into a terminal: xfreerdp /u:Administrator /p:grinch123! /v:$ip - The credentials for the machine are Administrator as the username, and grinch123! as the password.

Answer: `No answer needed`

### Question 2

Each transcription log is a simple plain text file that you can open in any editor of your choice. While the filenames are random, you can get an idea as to which log "comes first" by looking at the Date Modified or Date Created attributes, or the timestamps just before the file extension!

Open the first transcription log. You can see the commands and output for everything that ran within PowerShell, like whoami and systeminfo!

What operating system is Santa's laptop running ("OS Name")?

In: `PowerShell_transcript.LAPTOP._s3k_jad.20211128153510.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/2.png?raw=true)

Answer: `Microsoft Windows 11 Pro`

### Question 3

Review each transcription log to get an idea for what activity was performed on the laptop just after it went missing. In the "second" transcription log, it seems as if the perpetrator created a backdoor user account!

What was the password set for the new "backdoor" account?

In: `PowerShell_transcript.LAPTOP.k_dg27us.20211128153538`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/3.png?raw=true)

Answer: `grinchstolechristmas`

### Question 4

In one of the transcription logs,  the bad actor interacts with the target under the new backdoor user account, and copies a unique file to the Desktop. Before it is copied to the Desktop, what is the full path of the original file? 

In `PowerShell_transcript.LAPTOP.Zw6PA+c4.20211128153734.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/4.png?raw=true)

Answer: `C:\Users\santa\AppData\Local\Microsoft\Windows\UsrClass.dat`

### Question 5

The actor uses a Living Off The Land binary (LOLbin) to encode this file, and then verifies it succeeded by viewing the output file. What is the name of this LOLbin?

In `PowerShell_transcript.LAPTOP.Zw6PA+c4.20211128153734.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/5.png?raw=true)

Answer: `certutil.exe`

### Question 6

Read the above and open the ShellBagsExplorer.exe application found in the folder on your Desktop.

We can grab the content of the cert in `PowerShell_transcript.LAPTOP.Zw6PA+c4.20211128153734.txt` and place it in a second file:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/6.1.png?raw=true)

We can upload that in CyberChef using the `From Base64` tool.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/6.2.png?raw=true)

We can then download the result as `UsrClass.dat` then load it into ShellBags Explorer:

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/6.3.png?raw=true)

Answer: `No answer needed`

### Question 7

Drill down into the folders and see if you can find anything that might indicate how we could better track down what this SantaRat really is. What specific folder name clues us in that this might be publicly accessible software hosted on a code-sharing platform?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/7.png?raw=true)

Answer: `.github`

### Question 8

Additionally, there is a unique folder named "Bag of Toys" on the Desktop! This must be where Santa prepares his collection of toys, and this is certainly sensitive data that the actor could have compromised. What is the name of the file found in this folder? 

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/8.png?raw=true)

Answer: `bag_of_toys.zip`

### Question 9

What is the name of the user that owns the SantaRat repository?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/9.png?raw=true)

Answer: `Grinchiest`

### Question 10

Explore the other repositories that this user owns. What is the name of the repository that seems especially pertinent to our investigation?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/10.png?raw=true)

Answer: `operation-bag-of-toys`

### Question 11

Read the information presented in this repository. It seems as if the actor has, in fact, compromised and tampered with Santa's bag of toys! You can review the activity in the transcription logs. It looks as if the actor installed a special utility to collect and eventually exfiltrate the bag of toys. What is the name of the executable that installed a unique utility the actor used to collect the bag of toys?

In `PowerShell_transcript.LAPTOP.b+XfnW7t.20211128154858.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/11.png?raw=true)

Answer: `uharc-cmd-install.exe`

### Question 12

Following this, the actor looks to have removed everything from the bag of toys, and added in new things like coal, mold, worms, and more!  What are the contents of these "malicious" files (coal, mold, and all the others)?

In `PowerShell_transcript.LAPTOP.myCoN9lB.20211128155453.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/12.png?raw=true)

Answer: `GRINCHMAS`

### Question 13

We know that the actor seemingly collected the original bag of toys. Maybe there was a slight OPSEC mistake, and we might be able to recover Santa's Bag of Toys! Review the actor's repository for its planned operations... maybe in the commit messages, we could find the original archive and the password!

Answer: `No answer needed`

### Question 14

What is the password to the original bag_of_toys.uha archive? (You do not need to perform any password-cracking or bruteforce attempts)

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/14.png?raw=true)

Answer: `TheGrinchiestGrinchmasOfAll`

### Question 15

McSkidy was able to download and save a copy of the bag_of_toys.uha archive, and you have it accessible on the Desktop of the Windows analysis machine. After uncovering the password from the actor's GitHub repository, you have everything you need to restore Santa's original bag of toys!! 

Double-click on the archive on the desktop to open a graphical UHARC extraction utility that has been prepared for you. Using the password you uncovered, extract the contents into a location of your choosing (you might make a "Bag of Toys" directory on the Desktop to save all the files into).

With that, you have successfully recovered the original contents of Santa's Bag of Toys! You can view these in the Windows Explorer file browser to see how many were present.

How many original files were present in Santa's Bag of Toys?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day8/15.png?raw=true)

Answer: `228`