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

`ftp expose.thm` \
Signed in with Anonynmous and no password

FTP server appears to be empty. I am at the root directory and there are no files or folders, including hidden files/folders \
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/ab6f4987-9a1b-4470-8761-6590e708ee25)

Navigated to http://expose.thm:1337 in firefox browser. found a header of "EXPOSED" \
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/16c31d13-e099-4bcf-8198-be6d1a0e5dcd)

Page sourcecode shows that the header is the only thing on the page, network tab shows no other web requests were made.





