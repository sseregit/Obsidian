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