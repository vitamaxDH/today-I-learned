# LINEAR RAID 실습
- mdadm (Multiple Disk and Device Administration) : 디스크 여러개를 묶어서 RAID 로 만들어줌

### 실습 과정
- mdadm --create /dev/md9 --level=linear --raid-devices=2 /dev/sdb1 /dev/sdc1
- mdadm --detail --scan 으로 확인
- mkfs.ext4 /dev/md9 
- mkdir /raidLinear
- mount /dev/md9 /raidLinear

```
root@server:~# mdadm --create /dev/md9 --level=linear --raid-devices=2 /dev/sdb1 /dev/sdc1
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md9 started.
root@server:~# mdadm --detail --scan
ARRAY /dev/md9 metadata=1.2 name=server:9 UUID=03487a96:330f50e9:d7542dfc:5083072a
root@server:~# mkfs.ext4 /dev/m
mapper/ mcelog  md9     mem     mqueue/ 
root@server:~# mkfs.ext4 /dev/md9 
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 784896 4k blocks and 196224 inodes
Filesystem UUID: 82204e4e-5864-44ad-951c-9c8d50e16c4d
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 

root@server:~# mkdir /raidLinear
root@server:~# mount /dev/md9 /raidLinear/
root@server:~# df
Filesystem     1K-blocks    Used Available Use% Mounted on
udev             1971028       0   1971028   0% /dev
tmpfs             400068    1736    398332   1% /run
/dev/sda2       78106292 6709204  67386440  10% /
tmpfs            2000328       0   2000328   0% /dev/shm
tmpfs               5120       0      5120   0% /run/lock
tmpfs            2000328       0   2000328   0% /sys/fs/cgroup
/dev/loop0         56320   56320         0 100% /snap/core18/1705
/dev/loop1         56832   56832         0 100% /snap/core18/2074
/dev/loop2        246656  246656         0 100% /snap/gnome-3-34-1804/24
/dev/loop4         63616   63616         0 100% /snap/gtk-common-themes/1506
/dev/loop3        224256  224256         0 100% /snap/gnome-3-34-1804/72
/dev/loop5         66688   66688         0 100% /snap/gtk-common-themes/1515
/dev/loop6         51072   51072         0 100% /snap/snap-store/433
/dev/loop7         52224   52224         0 100% /snap/snap-store/547
/dev/loop8         27776   27776         0 100% /snap/snapd/7264
/dev/loop9         33152   33152         0 100% /snap/snapd/12398
tmpfs             400064      16    400048   1% /run/user/0
/dev/md9         3024752    9216   2842176   1% /raidLinear
```

- 재기동 후에도 적용해야함
- gedit /etc/fstab
- /dev/md9 /raidLinear ext4 defaults 0 0 추가