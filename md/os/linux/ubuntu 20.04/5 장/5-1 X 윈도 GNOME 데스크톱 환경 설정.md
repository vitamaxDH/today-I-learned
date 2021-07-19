# 배경화면 설정
- [GNOME 사진 사이트](https://www.gnome-look.org/broswe/cat)
- 테마 설정 : `apt -y install gnome-tweak-tool`
    - gnome-tweaks
- grub 화면 배경 : `apt -y install grub2-splashimages`
    - /usr/share/images/grub/ 의 이미지 파일 선택
    - gedit /etc/default/grub 파일에 GRUB_BACKGROUD=/usr/share/images/grub/... 추가
    - `update-grub` 적용 후 `reboot`
