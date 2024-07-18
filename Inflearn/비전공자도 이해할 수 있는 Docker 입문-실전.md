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