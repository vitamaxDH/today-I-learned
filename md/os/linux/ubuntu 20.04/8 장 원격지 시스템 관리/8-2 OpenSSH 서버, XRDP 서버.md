# OpenSSH 서버
- 텔넷과 용도는 동일하지만, 보안이 강화
- 텔넷과 거의 동일하지만 데이터를 전송할 때 암호화를 한다는 점이 다름

# OpenSSH 서버 구축
- 원격지에서 보안이 강화된 서버 접속할 경우 필요
- OpenSSH 서버 설치 과정 요약

1. ssh 서버 설치/가동
    - apt install openssh-server
    - systemctl restart ssh
2. 방화벽 설정
    - ufw allow 22/tcp
    1. 리눅스 클라이언트에서 접속
        - ssh 사용자명@서버IP
    2. Windows 클라이언트에서 접속 -> 3
3. 한글 Putty 실행
    - SSH 클라이언트 사용


# XRDP 서버
- X 윈도우 환경으로 원격접속을 사용하고 싶을 때
- Windows 의 `원격 데스크톱 연결` 프로그램을 사용해서 리눅스에 그래픽 환경으로 접속

1. XRDP 서버 설치
    - apt install xrdp (Remote Desktop Protocol)
2. 서비스 시작
    - systemctl restart xrdp
3. 방화벽 설정
    - ufw allow 3389/tcp
4. 윈도우에서 원격 데스크톱 연결(mstsc) 로 연결

