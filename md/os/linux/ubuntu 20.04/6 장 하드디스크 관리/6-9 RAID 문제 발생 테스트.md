## RAID 문제 발생 시키기
- setting 에서 각 레이드마다 disk 를 하나씩 제거한다.
- df, ll 등으로 확인해봐도 비정상적
- mdadm --detail --scan 으로 확인할 경우 INACTIVE 상태
```
root@server:~# mdadm --detail --scan
INACTIVE-ARRAY /dev/md5 metadata=1.2 name=server:5 UUID=a50fb296:84e7f963:3b4fd89c:aebd40d3
INACTIVE-ARRAY /dev/md1 metadata=1.2 name=server:1 UUID=8dfb04dc:8d830828:efaaf440:2192e716
INACTIVE-ARRAY /dev/md9 metadata=1.2 name=server:9 UUID=03487a96:330f50e9:d7542dfc:5083072a
INACTIVE-ARRAY /dev/md0 metadata=1.2 name=server:0 UUID=cf06238a:3c73acb2:572e5946:89b52b16
```
- md1 의 경우 복구 가능하기 때문에 mdadm --run /dev/md1 명령어를 통해 재기동
```
root@server:~# mdadm --run /dev/md1
mdadm: started array /dev/md1
root@server:~# mdadm --detail --scan
INACTIVE-ARRAY /dev/md5 metadata=1.2 name=server:5 UUID=a50fb296:84e7f963:3b4fd89c:aebd40d3
ARRAY /dev/md1 metadata=1.2 name=server:1 UUID=8dfb04dc:8d830828:efaaf440:2192e716
INACTIVE-ARRAY /dev/md9 metadata=1.2 name=server:9 UUID=03487a96:330f50e9:d7542dfc:5083072a
INACTIVE-ARRAY /dev/md0 metadata=1.2 name=server:0 UUID=cf06238a:3c73acb2:572e5946:89b52b16
root@server:~# 
```
- run 후 다시 마운트
    - mount /dev/md1 /raid1
- mdadm --detail /dev/md1 을 확인해보면 Active device 는 1개
```
root@server:~# mdadm --detail /dev/md1
/dev/md1:
           Version : 1.2
     Creation Time : Tue Aug  3 17:45:23 2021
        Raid Level : raid1
        Array Size : 1046528 (1022.00 MiB 1071.64 MB)
     Used Dev Size : 1046528 (1022.00 MiB 1071.64 MB)
      Raid Devices : 2
     Total Devices : 1
       Persistence : Superblock is persistent

       Update Time : Tue Aug  3 18:25:32 2021
             State : clean, degraded 
    Active Devices : 1
   Working Devices : 1
    Failed Devices : 0
     Spare Devices : 0

Consistency Policy : resync

              Name : server:1  (local to host server)
              UUID : 8dfb04dc:8d830828:efaaf440:2192e716
            Events : 19

    Number   Major   Minor   RaidDevice State
       0       8       49        0      active sync   /dev/sdd1
       -       0        0        1      removed
```
- raid 5 도 재기동 후 마운트
- mdadm --run /dev/md5
- mount /dev/md5 /raid5
- df
- gedit /etc/fstab 에서 md9 와 md0 을 주석처리
- 재기동 하여 df 로 확인