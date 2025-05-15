### 서버의 계정 확인하기
- `cat /etc/passwd`
	- 시스템에 존재하는 모든 사용자(시스템 포함)
- `awk -F: '$7 ~ /bash/ { print $1 }' /etc/passwd`
	- 로그인 가능한 일반 사용자
### 서버 계정 만들기
- `sudo adduser {유저명}`
	- 패스워드는 입력하라고 나온다.
	- 사용자 계정의 메타데이터를 입력하라고 나온다.
- `sudo usermod -aG sudo {유저명}`
	- sudo 권한 부여
### 서버 계정 삭제
- `sudo deluser --remove-home {유저명}`
	- `--remove-home`
		- `/home/ssh-test1`도 같이 지운다.
- `ps -u {계정명}`
	- 현재 사용자가 가상 터미널 세션이 열려있는지 확인한다.
		- `1862781 pts/2    00:00:00 bash`
		- TTY가 ? 인 경우 백그라운드에서 실행 중인 시스템/서비스 프로세스이다.
- `sudo loginctl terminate-user {유저명}`
	-  해당 세션을 깨끗하게 종료해준다.
### 리눅스 서버에서 사용할 수 있는 커맨드 확인
- `compgen -c | sort | uniq`