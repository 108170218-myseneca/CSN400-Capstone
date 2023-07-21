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

```bash
# FTP
iptables -A FORWARD -p tcp -d 172.17.18.36 --dport 21 -j LOG --log-prefix "Blocked FTP  packet: " --log-level 4
iptables -A FORWARD -p tcp -d 172.17.18.36 --dport 21 -j DROP

# SSH
iptables -A FORWARD -p tcp -d 172.17.18.37 --dport 22 -j LOG --log-prefix "Dropped SSH packet: " --log-level 4
iptables -A FORWARD -p tcp -d 172.17.18.37 --dport 22 -j DROP
```
### Part D - Azure Cost Analysis Charts


1. [./Images/Resource1.JPG](./Images/Resource1.JPG)

![DailyCosts Resource1](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Resource1.JPG)

2. [./Images/Service.JPG](./Images/Service.JPG)

![DailyCosts Service](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Service.JPG)

3. [./Images/Resource2.JPG](./Images/Resource2.JPG)

![DailyCosts Resource2](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Resource2.JPG)

4. [./Images/ServiceName.JPG](./Images/ServiceName.JPG)

![Service Name](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/ServiceName.JPG)

5. [./Images/ServiceFamily.JPG](./Images/ServiceFamily.JPG)

![Service Family](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/ServiceFamily.JPG)

6. [./Images/Product.JPG](./Images/Product.JPG)

![Last Month Product](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Product.JPG)

7. [./Images/Dashboard.JPG](./Images/Dashboard.JPG)

![Dashboard Sample-18](https://github.com/108170218-myseneca/CSN400-Capstone/blob/main/Checkpoint9/Images/Dashboard.JPG)









