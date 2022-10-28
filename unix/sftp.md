# SFTP commands
Instead of using the graphical tools like WinSCP, FileZilla etc and want to use the command line utility to access the FTP server then this document will help

If we want to connect to the FTP server using the username and password
```bash
$ sftp -oPort=10124 -oPreferredAuthentications=password admin@190.35.180.156
```

If we want to connect to the FTP server using the private key
```bash
$ sftp -o "IdentityFile=openssh.pk" user@remote.domain.com
```