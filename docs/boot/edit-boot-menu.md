# Modifying the boot meun on OpenIndiana

```
# list current boot menu(roughly, and location of it)
adrian@openindiana-hipster:~$ bootadm list-menu 
the location for the active GRUB menu is: /rpool/boot/grub/menu.lst
default 0
timeout 30
0 OI hipster
# Edit the boot menu accordingly and save
adrian@openindiana-hipster:~$ sudo nano /rpool/boot/grub/menu.lst 
# You're done, now just update the boot menu
adrian@openindiana-hipster:~$ sudo bootadm update-archive 
```

[![VIDEO](http://img.youtube.com/vi/8PDhVstTDTc/0.jpg)](https://www.youtube.com/watch?v=8PDhVstTDTc)
