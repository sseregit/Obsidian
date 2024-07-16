**최대한 CLI를 활용해 진행한다.**

homebrew를 이용한 docker 설치
`brew install docker`

- #error Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
	- docker daemon에 실행되지 않고 있다는 의미
	- `brew install --cask docker`
		- 앱을 설치해서 앱을 실행해야 한다.

[docker hub의 redis](https://hub.docker.com/_/redis)

redis 기본포트 6379 
docker의 포트는 (호스트 포트번호):(컨테이너 포트번호) 호스트 포트번호에 컨테이너 포트번호를 바인딩

`docker run --rm -p 6379:6379 redis`
`docker run --rm --name some-redis -d redis`

run
- 사용할 이미지가 저장되어 있는지 확인하고 없다면 다운로드(pull) 한 후 컨테이너를 생성(create)하고 시작(start)한다.
--rm 
- 프로세스 종료시 컨테이너 자동 제거
-p 
- 호스트와 컨테이너의 포트를 연결
--name
- 컨테이너 이름 설정

실행하고나서
[docker로 설치한 redis 접근](https://velog.io/@titu/Redis-docker%EB%A1%9C-%EC%84%A4%EC%B9%98%ED%95%9C-redis-%EC%A0%91%EA%B7%BC)

`docker exec -it (CONTAINER ID) redis-cli`
`docker exec -it (CONTAINER ID) redis-cli --raw`
exec
- run 명령어와 달리 실행중인 도커 컨테이너에 접속할 때 사용하며 컨테이너 안에 ssh server등을 설치하지 않고 exec 명령어로 접속한다.
--raw
- redis의 값들이 깨지지 않는다.

[Redis 설치(docker)와 redis-cli 사용법](https://hirlawldo.tistory.com/186)

redis-cli monitor 접근 방법
`docker exec -it (container id) redis-cli monitor`
-it
- -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션

`docker stop (container id)`
- -d 옵션을 사용할시 커맨드를 이용해 중지 해야한다.

`docker inspect (image name)`
- image name은 정확하지 않을 수 있다.

**보안 관련 문제는 Spring Data Redis를 익히고 찾는다**