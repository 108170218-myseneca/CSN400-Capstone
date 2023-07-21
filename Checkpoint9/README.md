# Checkpoint9 Submission

- **COURSE INFORMATION: CSN400-2234**
- **STUDENT’S NAME: Soufiane Berni**
- **STUDENT'S NUMBER: 108170218**
- **GITHUB USER ID: 108170218-myseneca**
- **TEACHER’S NAME: Atoosa Nasiri**

### Table of Contents

1. [Part A - Logging and Analyzing DNS and HTTP Traffic](#Part-A---Logging-and-Analyzing-DNS-and-HTTP-Traffic)
2. [Part B - Logging and Analyzing FTP and MySQL Traffic](#Part-B---Logging-and-Analyzing-FTP-and-MySQL-Traffic)
3. [Part C - Adjusting firewalls to DROP and LOG Traffic](#Part-C---Adjusting-firewalls-to-DROP-and-LOG-Traffic)
4. [Part D - Azure Cost Analysis Charts](#Part-D---Azure-Cost-Analysis-Charts)

### Part A - Logging and Analyzing DNS and HTTP Traffic

Logging and analyzing `DNS` and `HTTP` traffic using the tcpdump utility on `LR-18`. The goal is to create an `apache-iis.pcap` file and analysis it with `Wireshark`. After accessing to `IIS` and `Apache` pages from a Windows Client while `tcpdump` is running in the background. And after completing this steps and stoping the packet capture. Then, I filetered them to a specific packets to `apache-iis-filtered.pcap`, including `DNS`, `HTTP` requests, and replies between `Windows Client`, `IIS server`, and `Apache server`.

1. The commands that capture traffic in pcap format and direct it to a file is :

```bash
sudo tcpdump -i any -qnns 0 -w apache-iis.pcap "net 172.17.0.0/16" &
```
2. The commands that have transfer the apache-iis.pcap file to Windows Client is: 
```bash
scp -i sshkey.pem -P 22 192.168.18.36:~/apache-iis.pcap .
```
3. A screenshot of `apache-iis-filtered.pcap` that shows 8 packets.

![Apache Filtered](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/ApacheFiltered.JPG)

### Part B - Logging and Analyzing FTP and MySQL Traffic

Logging and analyzing `FTP` and `MySQL` traffic using the `tcpdump` utility on `LR-18`. The objective is to create an `ftp-mysql.pcap` file for analysis with Wireshark. Access `FTP` and `MySQL` pages from Windows Client while `tcpdump` runs in the background. After completing this step and stoping the packet capture. Including `DNS`, `MySQL` requests and replies, `FTP` requests and replies. And exporting them to `ftp-mysql-filtered.pcap` with only 8 packets.

1. The commands that capture traffic in pcap format and direct it to a file is :

```bash
sudo tcpdump -i any -qnns 0 -w ftp-mysql.pcap "net 172.17.0.0/16" &
```

2. The commands that have transfer the `ftp-mysql.pcap` file to Windows Client is:

```bash
scp -i sshkey.pem -P 22 192.168.18.36:~/ftp-mysql.pcap .
```
3. A screenshot of `ftp-mysql.pcap` that shows 8 packets.

![MySQL Filtered](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/MySQLFiltered.JPG)


### Part C - Adjusting firewalls to DROP and LOG Traffic

The `lr-drop-log.sh` file for firewalls to `DROP` and `LOG` Traffic:

[./logfile/lr-drop-log.log](./logfile/lr-drop-log.log)

```bash
# FTP
iptables -A FORWARD -p tcp -d 172.17.18.36 --dport 21 -j LOG --log-prefix "Blocked FTP  packet: " --log-level 4
iptables -A FORWARD -p tcp -d 172.17.18.36 --dport 21 -j DROP

# SSH
iptables -A FORWARD -p tcp -d 172.17.18.37 --dport 22 -j LOG --log-prefix "Dropped SSH packet: " --log-level 4
iptables -A FORWARD -p tcp -d 172.17.18.37 --dport 22 -j DROP
```


### click for the log content <<<<< lr drop log filtered log

<details>

<summary><b> output of the lr drop log filtered log</b></summary>

```bash
Jul 21 14:50:02 LR-18 kernel: TO_DROP_INPUTIN=eth0 OUT= MAC=00:22:48:d5:61:6a:12:34:56:78:9a:bc:08:00 SRC=40.87.164.0 DST=192.168.18.36 LEN=72 TOS=0x00 PREC=0x00 TTL=114 ID=0 DF PROTO=TCP SPT=23456 DPT=24449 WINDOW=17280 RES=0x00 ACK SYN URGP=0 
Jul 21 14:50:58 LR-18 kernel: TO_DROP_INPUTIN=eth0 OUT= MAC=00:22:48:d5:61:6a:12:34:56:78:9a:bc:08:00 SRC=40.87.172.0 DST=192.168.18.36 LEN=72 TOS=0x00 PREC=0x00 TTL=113 ID=0 DF PROTO=TCP SPT=23456 DPT=26486 WINDOW=17280 RES=0x00 ACK SYN URGP=0 
Jul 21 14:53:49 LR-18 waagent[6536]: 2023-07-21T14:53:49.518224Z INFO ExtHandler ExtHandler [HEARTBEAT] Agent WALinuxAgent-2.9.1.1 is running as the goal state agent [DEBUG HeartbeatCounter: 5;HeartbeatId: E07290F8-7C36-4940-AB9B-E28E73DCB163;DroppedPackets: 0;UpdateGSErrors: 0;AutoUpdate: 1]
Jul 21 14:55:02 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32443 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:02 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32444 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:02 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=112 TOS=0x00 PREC=0x00 TTL=127 ID=32445 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:03 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32446 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:03 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32447 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:03 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=184 TOS=0x00 PREC=0x00 TTL=127 ID=32448 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:04 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=184 TOS=0x00 PREC=0x00 TTL=127 ID=32449 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:05 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32450 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:05 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32451 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:05 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32452 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:05 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=292 TOS=0x00 PREC=0x00 TTL=127 ID=32453 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:06 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32454 PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:07 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=328 TOS=0x00 PREC=0x00 TTL=127 ID=32455 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:08 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32456 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:09 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=364 TOS=0x00 PREC=0x00 TTL=127 ID=32457 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:14 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=364 TOS=0x00 PREC=0x00 TTL=127 ID=32458 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:14 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32459 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:21 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32460 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:22 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32461 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:23 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=76 TOS=0x00 PREC=0x00 TTL=127 ID=32462 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=2049 RES=0x00 ACK PSH URGP=0 
Jul 21 14:55:24 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=40 TOS=0x00 PREC=0x00 TTL=127 ID=32463 DF PROTO=TCP SPT=50951 DPT=22 WINDOW=0 RES=0x00 ACK RST URGP=0 
Jul 21 14:55:29 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=32464 DF PROTO=TCP SPT=51103 DPT=22 WINDOW=64240 RES=0x00 SYN URGP=0 
Jul 21 14:55:30 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=32465 DF PROTO=TCP SPT=51103 DPT=22 WINDOW=64240 RES=0x00 SYN URGP=0 
Jul 21 14:55:32 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=32466 DF PROTO=TCP SPT=51103 DPT=22 WINDOW=64240 RES=0x00 SYN URGP=0 
Jul 21 14:55:36 LR-18 kernel: Dropped SSH packet: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.37 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=32467 DF PROTO=TCP SPT=51103 DPT=22 WINDOW=64240 RES=0x00 SYN URGP=0 
Jul 21 15:03:42 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45482 DF PROTO=TCP SPT=51161 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:03:43 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45483 DF PROTO=TCP SPT=51161 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:03:45 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45485 DF PROTO=TCP SPT=51161 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:03:49 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45489 DF PROTO=TCP SPT=51161 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:03:57 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45495 DF PROTO=TCP SPT=51161 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:00 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45498 DF PROTO=TCP SPT=51163 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:01 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45500 DF PROTO=TCP SPT=51163 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:03 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45502 DF PROTO=TCP SPT=51163 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:07 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45505 DF PROTO=TCP SPT=51163 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:07 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45506 DF PROTO=TCP SPT=51164 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:08 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45508 DF PROTO=TCP SPT=51164 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:10 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45510 DF PROTO=TCP SPT=51164 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:14 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45513 DF PROTO=TCP SPT=51164 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
Jul 21 15:04:22 LR-18 kernel: Blocked FTP TO WS-18: IN=eth0 OUT=eth0 MAC=00:22:48:d5:61:6a:c0:d6:82:70:fb:15:08:00 SRC=10.9.215.4 DST=172.17.18.36 LEN=52 TOS=0x00 PREC=0x00 TTL=127 ID=45518 DF PROTO=TCP SPT=51164 DPT=21 WINDOW=64240 RES=0x00 SYN URGP=0
```

</details>


![No Drop Log](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/NodropFiltered.JPG)


![Last Month Product](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Product.jpg)


### Part D - Azure Cost Analysis Charts


1. [./Images/Resource1.JPG](./Images/Resource1.JPG)

![DailyCosts Resource1](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Resource1.JPG)

2. [./Images/Service.JPG](./Images/Service.JPG)

![DailyCosts Service](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Service.JPG)

3. [./Images/Resource2.JPG](./Images/Resource2.JPG)

![DailyCosts Resource2](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Resource2.JPG)

4. [./Images/ServiceName.jpg](./Images/ServiceName.jpg)

![Service Name](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/ServiceName.jpg)

5. [./Images/ServiceFamily.JPG](./Images/ServiceFamily.JPG)

![Service Family](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/ServiceFamily.JPG)

6. [./Images/Product.jpg](./Images/Product.jpg)

![Last Month Product](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Product.jpg)

7. [./Images/Dashboard.JPG](./Images/Dashboard.JPG)

![Dashboard Sample-18](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Dashboard.JPG)









