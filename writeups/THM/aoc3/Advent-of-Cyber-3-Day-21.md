# Advent of Cyber - Day 21

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

We changed the text in the string $a as shown in the eicaryara rule we wrote, from X5O to X50, that is, we replaced the letter O with the number 0. The condition for the Yara rule is `$a and $b and $c and $d`. If we are to only make a change to the first boolean operator in this condition, what boolean operator shall we replace the 'and' with, in order for the rule to still hit the file?

Answer: `or`

### Question 2

What option is used in the Yara command in order to list down the metadata of the rules that are a hit to a file?

Answer: `-m`

### Question 3

What section contains information about the author of the Yara rule?

Answer: `metadata`

### Question 4

What option is used to print only rules that did not hit?

From the [documentation](https://yara.readthedocs.io/en/stable/commandline.html?highlight=print):

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day21/4.png?raw=true)

Answer: `-n`

### Question 5

Change the Yara rule value for the `$a` string to `X50`. Rerun the command, but this time with the -c option. What is the result?

YARA file: 

```yara
rule eicaryara   {
    meta:
      author="tryhackme"
      description="eicar string"
    strings:
      $a="X5O"
      $b="EICAR"
      $c="ANTIVIRUS"
      $d="TEST"
    condition:
      $a and $b and $c and $d
  }
```

Command: `yara -c eicaryara testfile`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day21/6.png?raw=true)

Answer: `0`
