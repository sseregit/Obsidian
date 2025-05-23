[sshj-github](https://github.com/hierynomus/sshj)
[java-sshj 사용](https://www.baeldung.com/java-sshj-ssh-library)
[ssh-setup-public-key](https://www.baeldung.com/linux/ssh-setup-public-key-auth)
****
# 1-1. 아이디/패스워드 방식 접속
## 1-1-1 ssh 사용자 계정 만들기
- [[ssh 사용자계정관련 커맨드?]]
## 1-1-2 sshj로 자바로 접속하기

# 1-2. 키 기반 접속 (다양한 키 포맷 처리)
## 1-2-1 키 기반 생성하기.
- SSH 키 인증 방식 알고리즘 RSA, ED25519 사용하기
	- 불가능 대상 서버에 OpenSSH 버전을 체크할 방법이 없음
	- RSA는 무조건 가능하니 RSA로만 테스트하기.

| 특성      | RSA (4096비트) | ED25519   |
| ------- | ------------ | --------- |
| 보안 수준   | 높음           | 매우 높음     |
| 성능      | 느림           | 빠름        |
| 키 크기    | 큼            | 작음        |
| 호환성     | 매우 높음        | 제한적일 수 있음 |
| 랜덤성 의존성 | 있음           | 없음        |
| 사용 역사   | 오래됨          | 비교적 최근    |
[[ssh 키기반 관련 커맨드?]]

# 1-3. 호스트 키 검증 방식 (KnownHosts 방식 적용)
## 1-3-1 키기반 접속과 호스트 키 검증 방식의 차이점
- `ssh-keyscan {원격 서버} >> ~/.ssh/known_hosts`
	- 원격 서버에 호스트 공개키를 받아와서 저장할수있음.
	- 로그인 인증 없이 호스트 공개키를 수동으로 등록하는 방법
- 이 궁금점 자체가 호스트키와 키기반을 약간 동일한 선상에 두고 판단한거였고
- 호스트키는 ssh를 사용하는 서버라면 무조건 생성이 되어있다.
	- ssh를 통해 ID/Password or rsa를 활용한 연결을 한번이라도 하면 client 서버 `.ssh/known_host`에 원격서버 호스트키가 저장된다.
	- 혹은 위에 방식으로 수동으로 등록할 수도 있다.
# 1-4. 인증 실패 시 재시도, 실패 횟수 제한 정책
### 예상되는 실패 시나리오
#### 세팅 실패 (Throwable, 해당 실패는 실행이 되면 안됨)
1. known_hosts 파일 존재 여부
2. RSA 개인키 파일 존재 여부
3. RSA 개인키 파일의 권한 확인
4. RSA 키 포맷 손상 여부   
#### 실행중 실패 (Exception)
1. host가 틀림 (DNS resolution 실패 or IP 오입력)
2. username이 틀림 (계정 없음)
3. RSA 개인키 틀림 (비밀번호가 필요한 암호화된 키인데 비밀번호 없음 등)
4. known_hosts에 등록되어 있지 않음
5. 원격 서버가 죽어 있음 (Connection refused / No route to host)
6. 명령어 실행 중 세션 종료 또는 실패 (ex: shell 접근 권한 없음, command not found)
7. ==사용자 계정에 ssh 로그인 권한이 없거나 nologin 쉘 지정됨==
8. ==서버에서 최대 세션 수 초과 (MaxSessions 제한 등)==
9. 네트워크 연결 중단 (Wi-Fi 끊김 등)
10. ==서버 호스트키 변경 감지 (HostKeyMismatchException)==

==해당 예외는 실제 프로젝트에 옮기면서 처리==
#### sshj?
1. java.net.ConnectException: Operation timed out
	1. 지정된 시간 내에 응답을 받지 못한 상태
2. java.net.BindException: Permission denied
	1. 특정 포트에 바인딩 하려 할 때 권한이 부족
3. java.net.SocketException: Network is unreachable
	1. 클라이언트 시스템이 대상 네트워크에 접근할 수 없을 때
4. java.net.ConnectException: Connection refused
	1. 연결을 시도 했지만, 해당 포트에서 수신 대기 중인 서브시가 없을 때 발생
5. java.net.UnknownHostException: 999.999.999.999