# Advent of Cyber 4 - Day 19

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What is the flag value after reversing the file firmwarev2.2-encrypted.gpg?

`cd bin`

`binwalk -E -N firmwarev2.2-encrypted.gpg`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.1.png?raw=true)

It's encrypted so we go to the older version:

`cd ../bin-unsigned`

We run the firmware extractor on it:

`extract-firmware.sh firmwarev1.0-unsigned`

This yields many files in the `fmk` folder.

We find the GPG keys and the paraphrase using grep: `grep -ri key` and `grep -ri paraphrase`, respectively in `fmk/rootfs/gpg` and `Santa@2022`.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.2.png?raw=true)

We load the private key: `gpg --import fmk/rootfs/gpg/private.key` and input the paraphrase.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.3.png?raw=true)

We load the public key: `gpg --import fmk/rootfs/gpg/public.key`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.4.png?raw=true)

We then list the available keys: `gpg --list-secret-keys`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.5.png?raw=true)

We move to `cd ../bin` and decrypt the firmware with the secret key: `gpg firmwarev2.2-encrypted.gpg`:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.6.png?raw=true)

We then enter `fmk/rootfs` to find `flag.txt` or we run `grep -ri thm` to find the flag:

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.7.png?raw=true)

Answer: `THM{WE_GOT_THE_FIRMWARE_CODE}`

### Question 2

> What is the Paraphrase value for the binary firmwarev1.0_unsigned?

We saw this in Question 1.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/1.2.png?raw=true)

Answer: `Santa@2022`

### Question 3

> After reversing the encrypted firmware, can you find the build number for rootfs?

From `fmk/rootfs` we run `ls -lah *` and find the build number.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day20/3.png?raw=true)

Answer: `2.6.31`
