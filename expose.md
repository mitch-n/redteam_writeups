Platform: TryHackMe \
Room: Expose \
URL: https://tryhackme.com/r/room/expose \
Date: 6/6/2024 \

# Notes

8:46 am \ 
Target: 10.10.71.102 \

Added expose.thm to /etc/hosts

`nmap -F expose.thm` \
Found ports 21,22,53

`rustscan -a 10.10.71.102`  \
Found additional ports 1337,1883

`nmap -p 21,22,53,1337,1883 -sV expose.thm`\
Output
```
PORT     STATE SERVICE                 VERSION
21/tcp   open  ftp                     vsftpd 2.0.8 or later
22/tcp   open  ssh                     OpenSSH 8.2p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
53/tcp   open  domain                  ISC BIND 9.16.1-Ubuntu
1337/tcp open  http                    Apache httpd 2.4.41 ((Ubuntu))
1883/tcp open  mosquitto version 1.6.9
MAC Address: 02:3B:23:EE:C4:FF (Unknown)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```


