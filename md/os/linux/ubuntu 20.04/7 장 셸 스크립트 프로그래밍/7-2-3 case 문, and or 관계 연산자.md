## case~esac 문 (1)
- if 문은 참과 거짓의 두 경우만 사용 (2중 분기)
- 여러 가지 경우의 수가 있다면 case 문 (다중분기)

> case1.sh
```bash
#!/bin/sh
case "$1" in
  start)
    echo "시작~~";;
  stop)
    echo "중지~~";;
  restart)
    echo "다시 시작~~";;
  *)
    echo "뭔지 모름~~";;
esac
exit 0
```
```
root@server:~# ./case1.sh restart
다시 시작~~
```

## case~esac 문 (2)
```bash
#!/bin/sh
echo "리눅스가 재미있나요? (yes/no)"
read answer
case $answer in
  yes|y|Y|Yes|YES)
    echo "다행입니다."
    echo "더욱 열심히 하세요 ^^";;
  [nN]*)
    echo "안타깝네요.ㅠㅠ";;
  *)
    echo "yes 아니면 no만 입력했어야죠"
    exit 1;;
esac
exit 0
```
```
root@server:~# ./case2.sh 
리눅스가 재미있나요? (yes/no)
y
다행입니다.
더욱 열심히 하세요 ^^
root@server:~# ./case2.sh 
리눅스가 재미있나요? (yes/no)
N 
안타깝네요.ㅠㅠ
root@server:~# ./case2.sh 
리눅스가 재미있나요? (yes/no)
k
yes 아니면 no만 입력했어야죠

```

## AND, OR 관계 연산자
---
- and 는 '-a' 또는 '&&' 를 사용
- or는 '-o' 또는 '||' 를 사용

```bash
#!/bin/sh
echo "보고 싶은 파일명을 입력하세요."
read fname
if [ -f $fname ] && [ -s $fname ]; then
  head -5 $fname
else
  echo "파일이 없거나, 크기가 0입니다."
fi
exit 0
```
```
root@server:~# ./andor.sh 
보고 싶은 파일명을 입력하세요.
/lib/systemd/system/nofileservice
파일이 없거나, 크기가 0입니다.
root@server:~# ./andor.sh 
보고 싶은 파일명을 입력하세요.
/lib/systemd/system/cron.service
[Unit]
Description=Regular background program processing daemon
Documentation=man:cron(8)
After=remote-fs.target nss-user-lookup.target
```
