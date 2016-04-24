# Removing old ZFS system snapshots


```bash

adrian@openindiana-tuts:~$ zfs list # lists your current zfs snapshots
NAME                       USED  AVAIL  REFER  MOUNTPOINT
rpool                     6.53G  24.2G    30K  /rpool
rpool/ROOT                4.98G  24.2G    19K  legacy
rpool/ROOT/openindiana    30.2M  24.2G  4.25G  /
rpool/ROOT/openindiana-1  4.95G  24.2G  4.25G  /
rpool/dump                 767M  24.2G   767M  -
rpool/export               360K  24.2G    19K  /export
rpool/export/home          341K  24.2G    19K  /export/home
rpool/export/home/adrian   322K  24.2G   322K  /export/home/adrian
rpool/swap                 816M  24.9G   120M  -
adrian@openindiana-tuts:~$ # the snapshot we want to get rid of is rpool/ROOT/openindiana
adrian@openindiana-tuts:~$ # since that is the snapshot without updates on it
adrian@openindiana-tuts:~$ # to do so we just type
adrian@openindiana-tuts:~$ sudo zfs destroy rpool/ROOT/openindiana #this should remove the old image
Password:
adrian@openindiana-tuts:~$ zfs list
NAME                       USED  AVAIL  REFER  MOUNTPOINT
rpool                     6.50G  24.3G    30K  /rpool
rpool/ROOT                4.95G  24.3G    19K  legacy
rpool/ROOT/openindiana-1  4.95G  24.3G  4.25G  /
rpool/dump                 767M  24.3G   767M  -
rpool/export               360K  24.3G    19K  /export
rpool/export/home          341K  24.3G    19K  /export/home
rpool/export/home/adrian   322K  24.3G   322K  /export/home/adrian
rpool/swap                 816M  24.9G   120M  -
adrian@openindiana-tuts:~$ # we have now removed the snapshot!

```
