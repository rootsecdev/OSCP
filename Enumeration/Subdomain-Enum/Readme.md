# Subdomain enumeration

Hunting for domains and subdomain using dig. DNS is required to be running on the target box for this to work. This command essential attempts to do an unauthenticated domain zome transfer. 

```
dig axfr @10.10.10.13 cronos.htb
```

You can also hunt for subdomains with fuff. Example with filtering http resonse size:

```
ffuf -u http://domain.local -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H 'Host: FUZZ.domain.local' -fs 0 -fs 65
```

DNS recon:
```
dnsrecon -t brt -d acmeitsupport.thm
```

Sublist3r example:
```
./sublist3r.py -d acmeitsupport.thm
```

Using ffuf
```
ffuf -w /usr/share/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.28.190
```

If you get a bunch of 200 status back use the filter size switch
```
ffuf -w /usr/share/seclists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.28.190 -fs 2395
```

## Websites for subdomain enum

Certsh
```
https://crt.sh/
```

Certificate Transparance Tool:
```
https://ui.ctsearch.entrust.com/ui/ctsearchui
```
