# Root 분실 시
- restart 하면서 esc 강타
- GNU GRUB 화면에서 *Ubuntu 선택 후 'e'
- linux    /boot 에 커서를 옮긴 후 'end' 키
- init=/bin/bash 추가 후 Ctrl + x (재부팅)
- whoami 로 사용자 확인
- passwd 로 변경 시도 -> `실패`

>현재는 응급복구 모드이기 때문에 READ 만 가능

- mount -o remount,rw / 를 넣어 write 모드 추가
- passwd 로 비밀번호 변경

하지만 위는 위험하기 때문에 `GRUB` 화면에도 비밀번호를 추가 설정
더 나아가 `SIMOS`, `BIOS` 에도 비밀번호를 추가해줄 수 있다.

# GRUB 부트로더 (GRand Unified Bootloader)
## 1. GRUB 부트로더의 특징
- 부트 정보를 사용자가 `임의로 변경`해 부팅할 수가 있다. 즉, 부트 정보가 올바르지 않더라도 수정하여 부팅할 수 있다.
- 다른 `여러 가지 운영체제`와 `멀티부팅`을 할 수 있따.
- 대화형 설정을 제공해줘서, 커널의 경로와 파일 이름말 알면 부팅이 가능하다.
## 2. GRUB2의 장점
- `셸 스크립트`를 지원. 조건/함수 사용 가능
- `동적 모듈 로드` 가능
- `그래픽` 부트 메뉴, 부트 스플래시 성능 개선
- ISO 이미지 이용하여 바로 부팅 가능

## 3. 설정 방법
- `/boot/grub/grub.cfg` (직접 변경x)
- `/etc/default/grub` 및 `/etc/grub.d/` 파일 수정 후 `update-grub` 커맨드

- `/etc/grub.d/00_header` 파일의 최하단에 추가
```
cat << EOF
set superusers="grubuser"
password grubuser 4321
EOF
```
