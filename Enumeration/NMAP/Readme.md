# NMAP:

Legend: 
```
-PS/PA/PU/PY[portlist]: TCP SYN/ACK, UDP or SCTP discovery to given ports
-PM: option required to tell Nmap to use ICMP Address Mask to discover live hosts
-PP: option tells Nmap to use ICMP timestamp requests
-PE: use ICMP echo request to discover live hosts
-PR: indicates that you only want an ARP scan
-sn: discover online hosts without port-scanning the live systems
-sL: List Scan - simply list targets to scan
-sN TCP Null Scan reveals the status of ports without directly querying them
-sV: Probe open ports to determine service/version info
-sC: equivalent to --script=default
-sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
-sU: UDP Scan
-O: Enable OS detection
-g/--source-port <portnum>: Use given port number
-oA <basename>: Output in the three major formats at once
-A: Enable OS detection, version detection, script scanning, and traceroute
-n/-R: Never do DNS resolution/Always resolve [default: sometimes]
--version-light: Limit to most likely probes (intensity 2)
```

NMAP Discovery using ARP (Commands will only discover assets on the same subnet)

```
sudo nmap -PR -sn 10.10.210.6/24
```



Examples Commands:


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

Other Examples:

```
sudo nmap -PA -sn 10.10.68.220/24
```

```
sudo nmap -PU -sn 10.10.68.220/24
```
