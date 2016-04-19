# Mounting NFS shares in OpenIndiana

This tutorial assumes you already have a running NFS server.

```bash
adrian@openindiana-hipster:~$ sudo mkdir -p /media/adrian/nfs/storage # make the dir to mount the share to.
adrian@openindiana-hipster:~$ sudo chown adrian:staff -R /media/adrian # apply ownership of dirs if you want
adrian@openindiana-hipster:~$ sudo mount -F nfs 192.168.0.103:/storage /media/adrian/nfs/storage # mount the share
adrian@openindiana-hipster:~$ df -h #hold your breath!
rpool/ROOT/openindiana-1   28G  4.3G   24G  16% /
swap                      1.1G  448K  1.1G   1% /etc/svc/volatile
swap                      1.3G  129M  1.1G  11% /tmp
swap                      1.1G   76K  1.1G   1% /var/run
rpool/export               24G   19K   24G   1% /export
rpool/export/home          24G   19K   24G   1% /export/home
/export/home/adrian        24G   43M   24G   1% /home/adrian
rpool                      24G   30K   24G   1% /rpool
192.168.0.103:/storage    298G  128G  170G  43% /media/adrian/nfs/storage
adrian@openindiana-hipster:~$ ls -l /media/adrian/nfs/storage # we can see our share is mounted.
total 68760
-rw-rw-r--   1 1000 1000 70308678 Jul 24 00:09 atom-amd64.deb
drwxrwxr-x+  7 1000 1000     4096 Sep  9 21:10 Backup
drwxrwxr-x+  2 1000 1000        1 Sep  3 00:28 build
drwxrwxr-x+  3 1000 1000        8 Jul 27 12:41 C-stuff
drwxrwxr-x+  2 1000 1000     4096 Apr  1  2015 cc
drwxrwxr-x+  9 1000 1000     4096 Oct 10 23:36 docker
drwxrwxr-x+ 11 1000 1000     4096 Oct  9 00:16 Downloads
drwxrwxr-x+ 11 1000 1000     4096 Oct 10 22:45 sites
lrwxrwxrwx   1 1000 1000       41 May 15 20:46 soulseek-downloads -> /home/adrian/Downloads/soulseek-downloads
lrwxrwxrwx   1 1000 1000       39 May 15 20:46 soulseek-uploads -> /home/adrian/Downloads/soulseek-uploads
drwxrwxr-x+  5 1000 1000     4096 Oct 11 14:56 virtualboxVMS
adrian@openindiana-hipster:~$ sudo umount /media/adrian/nfs/storage # unmounting is super easy!
```


[![video](http://img.youtube.com/vi/gyKhbDJk3LM/0.jpg)](https://www.youtube.com/watch?v=gyKhbDJk3LM)
