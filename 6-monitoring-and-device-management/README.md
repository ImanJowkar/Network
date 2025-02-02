## PASSWORD 

```



```

# Disk 
```
more system:running-config

show file systems

## FTP
! works on  20/tcp  and   21/tcp

conf t
ip ftp username test
ip ftp password test
exit
copy startup-config ftp://192.168.229.171/myrunbackup

copy ftp://ftpuser:ftpuser@192.168.229.171/myrunbackup unix:test






## TFTP 
!works on 69/udp

copy running-config tftp://192.168.229.170/backup
copy startup-config tftp://192.168.229.170/run

copy tftp://192.168.229.170/run running-config


# check md5sum of a ios file
verify /md5 flash:IOS
verify /md5 flash:IOS <hash>




```

