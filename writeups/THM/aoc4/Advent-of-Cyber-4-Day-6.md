# Advent of Cyber 4 - Day 6

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the email address of the sender?

We look at the `.eml` file for details, specificall the `From:` header.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/1.png?raw=true)

Answer: `chief.elf@santaclaus.thm`

### Question 2

> What is the return address?

We look at the `Return-Path:` header.

Answer: `murphy.evident@bandityeti.thm`

### Question 3

> On whose behalf was the email sent?

Once more, we look at the `From:` header.

Answer: `Chief Elf`

### Question 4

> What is the X-spam score?

We look at the `X-Pm-Spamscore:` header.

Answer: `3`

### Question 5

> What is hidden in the value of the Message-ID field?

We get the value in the field, notice it is base64 encoded, and get the decoded string using `echo -n "QW9DMjAyMl9FbWFpbF9BbmFseXNpcw==" | base64 -d`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/5.png?raw=true)

Answer: `AoC2022_Email_Analysis`

### Question 6

> Visit the email reputation check website provided in the task. What is the reputation result of the sender's email address?

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/6.png?raw=true)

Answer: `RISKY`

### Question 7

> Check the attachments. What is the filename of the attachment?

We process the `.eml` file using `emlAnalyzer` like so: `emlAnalyzer -i Urgent\:.eml --header --html -u --text --extract-all` (*make sure to be in the same directory as the `.eml` file*)

Then look under `Attachment Extracting`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/7.png?raw=true)

Answer: `Division_of_labour-Load_share_plan.doc`

### Question 8

> What is the hash value of the attachment?

We simply take the extracted file at `$PWD/eml_attachments/Division_of_labour-Load_share_plan.doc` and use `sha256sum` like so:

`sha256sum eml_attachments/Division_of_labour-Load_share_plan.doc`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/8.png?raw=true)

Answer: `0827bb9a2e7c0628b82256759f0f888ca1abd6a2d903acdb8e44aca6a1a03467`

### Question 9

> Visit the Virus Total website and use the hash value to search.
> Navigate to the behaviour section.
> What is the second tactic marked in the Mitre ATT&CK section?

After pasting the hash in VT, we need to go to the `BEHAVIOR` tab, and scroll down to find the `MITRE ATT&CK Tactics and Techniques`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/9.png?raw=true)

Answer: `Defense Evasion`

### Question 10

> Visit the InQuest website and use the hash value to search.
> What is the subcategory of the file?

After pasting the hash in InQuestLabs, we get a reference to the documentation for a malicious file. By clicking on this reference, we find the subcategory:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day6/10.png?raw=true)

Answer: `macro_hunter`