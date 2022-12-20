# Advent of Cyber - Day 16

Link: [Advent Of Cyber 3 on TryHackMe](https://tryhackme.com/room/adventofcyber3)

### Question 1

You are the responding intelligence officer on the hunt for more information about the infamous "Grinch Enterprises" ransomware gang. 
As a response to the recent ransomware activity from Grinch Enterprises, your team has managed to collect a sample ransomware note. 

```
!!! ВАЖНЫЙ !!!

Ваши файлы были зашифрованы Гринчем. Мы используем самые современные технологии шифрования.

Чтобы получить доступ к своим файлам, обратитесь к оператору Grinch Enterprises.

Ваш личный идентификационный идентификатор: «b288b97e-665d-4105-a3b2-666da90db14b».

С оператором, назначенным для вашего дела, можно связаться как "GrinchWho31" на всех платформах.

!!! ВАЖНЫЙ !!!
```

Answer: `No answer needed`

### Question 2

What is the operator's username?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/2.png?raw=true)

Answer: `GrinchWho31`

### Question 3

What social media platform is the username associated with?

Using [checkusernames.com](https://checkusernames.com/?username=GrinchWho31):

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/3.png?raw=true)

Answer: `Twitter`

### Question 4

What is the cryptographic identifier associated with the operator?

From [Twitter](https://twitter.com/GrinchWho31):

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/4.png?raw=true)

Answer: `1GW8QR7CWW3cpvVPGMCF5tZz4j96ncEgrVaR`

### Question 5

What platform is the cryptographic identifier associated with?

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/5.png?raw=true)

Answer: `keybase.io`

### Question 6

What is the bitcoin address of the operator?

From [Keybase](https://keybase.io/grinchwho31/sigs/1GW8QR7CWW3cpvVPGMCF5tZz4j96ncEgrVaR):

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/6.png?raw=true)

Answer: `bc1q5q2w2x6yka5gchr89988p2c8w8nquem6tndw2f`

### Question 7

What platform does the operator leak the bitcoin address on? 

This should be "Keybase" again, but it is apparently GitHub. Visit the [GitHub](https://github.com/christmashater31) mentioned in the previous task and go to the `Christmas-Stealer` repository and find the address.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/7.png?raw=true)

Answer: `GitHub`

### Question 8

What is the operator's personal email?

Go to the other repository's (`ChristBASHTree`) commit history, the latest commit removes some lines.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/8.png?raw=true)

Answer: `DonteHeath21@gmail.com`

### Question 9

What is the operator's real name?

See the previous question.

![](https://github.com/AtomicNicos/knowledge-base/blob/main/writeup_resources/aoc3/day16/9.png?raw=true)

Answer: `Donte Heath`