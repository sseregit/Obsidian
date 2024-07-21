[수업자료](https://jscode.notion.site/a9affdeece4b45efb1424835d9c2da46?pvs=4)

## Docker를 왜 배우는 걸까?

### 이식성
특정 프로그램을 다른 곳으로 쉽게 옮겨서 설치 및 실행할 수 있는 특성

## IP와 Port 개념

### IP
네트워크 상에서의 특정 컴퓨터를 가리키는 주소

### Port
실행되고 있는 특정 프로그램의 주소

## Docker란? / 컨테이너(Container)란? / 이미지(Image)란?

### Dock란?
컨테이너를 사용하여 각각ㄱ의 프로그램을 분리된 환경에서 실행 및 관리할 수 있는 툴이다.

### 컨테이너(Container)란?
하나의 컴퓨터 환경내에서 독립적인 컴퓨터 환경을 구성해서 미니 컴퓨터 환경을 구성할 수 있는 형태이다.

#### 호스트 컴퓨터
컨테이너를 포함하고 있는 컴퓨터

#### 독립성
- 디스크 (저장공간)
	- A 컨테이너 내부에서 B 컨테이너 내부에 있는 파일에 접근할 수 없다.
- 네트워크(IP, Port)
	- 각 컨테이너 마다 고유의 네트워크를 가지고 있다.

### 이미지(Image)란?
프로그램을 실행하는 데 필요한 모든 것을 포함하고 있다.

## Docker 전체 흐름 느껴보기 (Nginx 설치 및 실행)

## 이미지(Image) 다운로드

`docker pull <이미지:버전<필수아님>>`

## 이미지(Image) 조회/삭제

`docker image rm -f $(docker images -q)`
- -f
	- 실행중인 컨테이너를 제외하고 중지된 컨테이너의 이미지를 삭제할 수있다.
- $(docker images -q)
	- 시스템에 있는 모든 이미지의 ID를 반환한다
	- -q
		- quite를 의미하며 상세 정보 대신에 각 이미지의 고유한 ID만 표시하도록 지시한다.

## 컨테이너(Container) 생성 / 실행 - 1

`docker ps -a`
- 모든 컨테이너 조회

## 컨테이너(Container) 생성 / 실행 - 2

`docker run <image>`
- docker create , docker start 모두 하고 image가 없을시 pull 까지 한다.

#### 포그라운드(foreground)
내가 실행시킨 프로그램의 내용이 화면에서 실행되고 출력되는 상태

#### 백그라운드(background)
내가 실행시킨 프로그램이 컴퓨터 내부적으로 실행되는 상태를 의미한다

## 컨테이너(Container) 조회/중지/삭제

`docker stop <Container ID>`
컨테이너 중지

`docker kill <Container ID>`
컨테이너 강제 종료
강제로 종료하는 느낌이라 stop을 우선으로 사용한다.

`docker rm -f $(docker ps -qa)`
중단된 컨테이너 모두 삭제

## 컨테이너(Container) 로그 조회

`docker logs <Container id>`

`docker logs --tail 0 -f <Container id>`
- --tail 0
	- 과거의 log가 나오지않고
- -f
	- 실시간 로그부터 보기 시작한다

## 실행중인 컨테이너 내부에 접속하기 (exec -it)

`docker exec -it <Container id> bash`

`exit`
명령어로 bash에선 나온다

## Docker 전체 흐름 다시 느껴보기 (Nginx 설치 및 실행)

## Docker로 Redis 실행시켜보기

## Docker Volumne(도커 볼륨)

### 컨테이너가 가진 문제점
프로그램에 기능이 추가되면 새로운 이미지를 만들어서 컨테이너를 실행시켜야 하는데 Docker는 기존 컨테이너의 변경된 부분을 수정하지 않고, 새로운 컨테이너를 만들어서 통째로 갈아끼우는 방식으로 교체한다
그래서 기존 컨테이너 내부에 있던 데이터도 같이 삭제된다.

### Docker Volumne(도커 볼륨)이란?
도커 컨테이너에서 데이터를 영속적으로 저장하기 위한 방법
볼륨은 컨테이너 자체의 저장 공간을 사용하지 않고 호스트 자체의 저장 공간을 공유해서 사용하는 형태이다.

`docker run -v [호스트의 디렉토리 절대경로]:[컨테이너의 디렉토리 절대경로] [이미지명]:[태그명]`
#### 호스트 디렉토리가 이미 존재할 경우 
호스트의 디렉터리가 컨테이너의 디렉터리를 덮어씌운다

#### 호스트 디렉토리가 존재하지 않을 경우
호스트의 디렉터리 절대 경로에 디렉토리를 새로 만들고 컨테이너의 디렉터리에 있는 파일들을 호스트의 디렉토리로 복사해온다

## Docker로 MYSQL로 실행시켜보기 - 1

## Docker로 MYSQL로 실행시켜보기 - 2

## Docker로 MYSQL로 실행시켜보기 - 3

## Docker로 MYSQL로 실행시켜보기 - 4

## Docker로 PostgreSQL 실행시켜보기

## Docker로 MongoDB 실행시켜보기

## Dockerfile이란?

### Dockerfile이란?
Dockerfile을 활용해서 Docker 이미지를 만들 수 있다.

## FROM: 베이스 이미지 생성

### Dockerfile << 파일명

### FROM
베이스 이미지를 생성하는 역할을 한다

```dockerfile
FROM [이미지명]
FROM [이미지명]:[태그명]
```

## FROM: 베이스 이미지 생성

`docker build -t [이미지명]:[태그명] [Dockerfile 위치 경로]`
태그명이 존재하지 않으면 latest

## 종료된 컨테이너에 들어가서 디버깅하고 싶을 때
