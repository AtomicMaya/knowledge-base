# Advent of Cyber - Day 18

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

What command will list container images stored in your local container registry?

Answer: `docker images`

### Question 2

What command will allow you to save a docker image as a tar archive?

Answer: `docker save`

### Question 3

What is the name of the file (including file extension) for the configuration, repository tags, and layer hash values stored in a container image?

Answer: `manifest.json`

### Question 4

What is the token value you found for the bonus challenge?

Commands:
```bash
mkdir aoc
cd aoc
docker save -o aoc.tar public.ecr.aws/h0w1j9u3/grinch-aoc:latest
tar -xf aoc.tar
cat manifest.json | jq
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day18/4.1.png?raw=true)

Command: `cat f886f00520700e2ddd74a14856fcc07a360c819b4cea8cee8be83d4de01e9787.json | jq`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day18/4.2.png?raw=true)

Commands: 
```
cd 4416e55edf1a706527e19102949972f4a8d89bbe2a45f917565ee9f3b08b7682
grep -n "token" root/envconsul/config.hcl
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day18/4.3.png?raw=true)

Answer: `7095b3e9300542edadbc2dd558ac11fa`
