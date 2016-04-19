# Mirring Rpool

For safetys sake lets say you wanted to mirror your rpool, unfortunately this is not as straight forward as simply running.

```bash
adrian@openindiana-tuts:~$ sudo zpool attach rpool drive1 drive2
```
the full process is listed below.

Lets assume you have two disks c7t0d0and c7t1d0(where c7t0d0contains your current installation).

* Boot up gparted and ensure the second disk has no partitions(or your fave partition tool.)

* apply the default solaris2 partition to the disk

```bash
adrian@openindiana-tuts:~$ sudo fdisk -B c7t1d0p0
```
* Check the partition table (option 191 should say SUNIXOS2)

```
adrian@openindiana-tuts:~$ sudo fdisk -W - c7t1d0p0
```
4. Set the label on the second disk based on that of the first

```
adrian@openindiana-tuts:~$ sudo prtvtoc /dev/rdsk/c7t0d0s0 | fmthard -s - /dev/rdsk/c7t1d0s0
```

5. Attach the second disk to the rpool

```bash
adrian@openindiana-tuts:~$ sudo zpool attach -f rpool c7t0d0s0 c7t1d0s0
```
6. Wait for the resilver to finish

```bash
adrian@openindiana-tuts:~$ sudo zpool status
```
7. Install grub on the second disk

```bash
adrian@openindiana-tuts:~$ sudo installgrub /boot/grub/stage1 /boot/grub/stage2 /dev/rdsk/c7t1d0s0
```
8. Reboot and test booting from the other disk

```bash
adrian@openindiana-tuts:~$ sudo reboot
```
credit for these docs go to [/u/127b](https://www.reddit.com/user/127b)
