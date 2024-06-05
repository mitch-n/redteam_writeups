Platform: TryHackMe
Room: CyberLens
URL: https://tryhackme.com/r/room/cyberlensp6
Date: June 5, 2024

# Notes
10:21 am
Loaded target machine
IP 10.10.234.94

added cyberlens.thm to hosts file (mentioned in the room description)
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/dc1950a7-8a20-4dab-9752-f0bb18e66d02)

Fast NMAP scan of target. `nmap -F cyberlens.thm`
Found ports 80,135,139,445,3389

rustscan of target. `rustscan -a 10.10.234.94
Found ports 80,135,139,3389,445,5985,47001,49664,49665,49666,49667,49668,49669,49670,49671,61777

Running nmap service scan of all open ports `nmap -sV -p80,135,139,3389,445,5985,47001,49664,49665,49666,49667,49668,49669,49670,49671,61777 cyberlens.thm`
OUTPUT:
```
PORT      STATE SERVICE       VERSION
80/tcp    open  http          Apache httpd 2.4.57 ((Win64))
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp   open  microsoft-ds?
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49670/tcp open  msrpc         Microsoft Windows RPC
49671/tcp open  msrpc         Microsoft Windows RPC
61777/tcp open  http          Jetty 8.y.z-SNAPSHOT
```
Found HTTP servers on ports 80,5985,47001,61777

Opened firefox browser and burpsuite, proxying traffic

