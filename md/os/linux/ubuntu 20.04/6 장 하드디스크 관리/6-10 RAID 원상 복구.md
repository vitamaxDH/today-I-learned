## Linear RAID, RAID 0, 1, 5 원상 복구
- 실습 구성
    - 고장난 디스크 4개를 새 디스크로 교체
    - New disk 를 추가
- 자동으로 복구가 되지는 않음
- 처음 넣은 것처럼 깡통만 들어간 상황
- fdisk 를 통해 넣어줌
    - fdisk /dev/sdc ~ sdi
- mdadm --stop /dev/md9, /dev/md0  정지

### 복구가 불가능한 경우 (linear, raid 0)
- mdadm --create /dev/md9 --level=linear --raid-devices=2 /dev/sdb1 /dev/sdc1 등으로 다시 설정

### 복구가 가능한 경우 (raid 1, raid 5)
- mdadm /dev/md1 --add /dev/sdg1 등

<hr>

- gedit /etc/fstab 주석 해제
- reboot
- df
- md0, md9 이 없다면 mdadm --detail --scan 으로 검색하고, 뒤에 붙는 server:0, server:9 등을 /etc/fstab 에 알맞게 변경해준다.