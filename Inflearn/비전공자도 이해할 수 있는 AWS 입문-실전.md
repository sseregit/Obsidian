[수업자료](https://jscode.notion.site/2a38dc67ca1448f7ab350e40b89abd5a)

## 배포(Deployment)란?
- 다른 사용자들이 인터넷을 통해서 사용할 수 있게 만드는 걸 의미한다.

## ES2란? / ES2를 왜 배울까? / 현업에서 EC2는 주로 언제 쓸까?

### EC2란?
	Elastic Compute Cloud
	컴퓨터를 빌려서 원격으로 접속해 사용하는 서비스이다.

### ES2를 왜 배울까?
	AWS EC2의 여러 부가기능(로깅, 오토스케일링, 로드밸런싱등등..)

### 현업에서는?
	백엔드 서버를 배포할 때면 EC2에 서버를 배포해서 사용한다.
	주로 백엔드 위주로 배포하는데 사용한다
	프론트엔드 웹 페이지를 배포할때는 ?
		AWS EC2보다는 vercel, netlify, AWS S3를 사용해서 주로 배포한다.

## EC2 셋팅하기 - 리전(Region) 선택

### 리전(Region)
	인프라를 지리적으로 나누어 배포한 각각의 데이터 센터
- 특징
	- 각 Region은 고유의 이름을 가지고 있다.
- 어떤 기준으로 선택할까?
	- 애플리케이션의 주된 사용자들의 위치와 지리적으로 가까운 리전(Region)을 선택하는 것이 유리하다.
- 많이 하는 실수
	- 아시아 태평양(서울) 리전에서 EC2를 생성해놓고, 다른 나라 리전에 들어가서 생성한 EC2가 없어졌다고 당황하는 경우가 있다.
	- 리전(Region)마다 EC2가 따로따로 관리가 되고 있으니 이 점 유의하자

## EC2 셋팅하기 - 기본 설정

EC2 > 인스턴스 > 인스턴스 시작

이름 및 태그
	인스턴스를 식별할 수 있는 값

Application and OS Images
	사용할 OS를 선택한다.

인스턴스 유형
	인스턴스란
		EC2에서 빌리는 서버의 하나
	유형
		컴퓨터 사양

키페어(로그인)
	키페어
		EC2에 접근할 때 사용하는 Key

## EC2 셋팅하기 - 보안그룹 설정

네트워크 설정

보안그룹(Security Group)
	AWS 클라우드에서의 네트워크 보안을 의미한다.
	보안 규칙
		인바운드 트래픽
			외부에서 EC2 인스턴스로 보내는 트래픽
		아웃바운드 트래픽
			EC2 인스턴스에서 외부로 나가는 트래픽
	ssh
		EC2 원격 접속을 위한

## IP와 Port 개념

IP
	네트워크 상에서 특정 컴퓨터를 가리키는 주소

Port
	한 컴퓨터 내에서 실행되고 있는 특정 프로그램의 주소

well-known port
	0 ~ 1023번 까지의 포트 번호는 주요 통신을 위한 규약에 따라 이미 정해져 있다.
	ex)
		22번
			원격 접속을 위한 포트 번호
		80번
			HTTP로 통신을 할 때 사용
		443번
			HTTPS로 통신을 할 때 사용

## EC2 셋팅하기 - 스토리지 구성

스토리지 구성
	EBS(Elastic Block Storage)
		EC2 안에 부착되어 있는 일종의 하드디스크
		스토리지, 볼륨이라고 좀더 포괄적인 용어로도 부른다.

## EC2 접속하기

### 퍼블릭 IPv4 주소
외부 접근 가능 주소

### 인스턴스 상태
#### 중지
종료
#### 시작
시작

#### 재부팅
재부팅

#### 종료
해당 인스턴스 삭제

## 탄력적 IP 연결하기

EC2 인스턴스를 생성하면 IP를 할당받지만 임시적인 IP로 다시 중지후 실행하면 IP가 변경된다 그래서 다시 실행해도 변경되지 않는 고정 IP를 할당받아야 한다
그것이 **탄력적 IP**

## Express 서버를 EC2에 배포하기

## Spring Boot 서버를 EC2에 배포하기

## 비용 나가지 않게 EC2 깔끔하게 종료하기
### 인스턴스를 종료(삭제)한다
### 탄력적IP도 릴리즈 한다

## Route53이란?/ DNS란? / 현업에서의 Route53 활용 여부

### Route53
도메인을 발급하고 관리해주는 서비스

### DNS(Domain Name System)

### 현업에서의 Route53 활용여부
IP주소에는 HTTPS를 적용을 할 수가 없다.
도메인주소가 있어야 HTTPS가 있어야 한다.
Route53외에도 가비아, 후이즈 등에서도 도메인을 구매하고 관리할 수 있다.

## Route53에 연결할 EC2 생성하기

IP사용의 문제점
1. IP를 외우기 힘들다
2. IP에는 HTTPS를 적용할 수 없다.

## Route53에서 도메인 구매

## Route53의 도메인을 EC2에 연결하기

## 무료로 도메인 구매하는 방법

[내도메인.한국](https://xn--220b31d95hq8o.xn--3e0b707e/)

무료도메인의 단점
도메인서버 자체가 불안하다

## ELB란? TLS, SSL와 HTTPS

### ELB (Elastic Load Balancer)
트래픽(부하)을 적절하게 분배해주는 장치

### SSL/TLS란?
HTTP를 HTTPS로 바꿔주는 인증서

### HTTPS
1. 보안적인 이유
	1. 데이터를 암호화 시켜 통신을 한다.
2. 사용자 이탈

### 현업에서는?
대부분 웹사이트에서 HTTPS를 적용시킨다.
HTTPS 인증을 받은 웹 사이트가 백엔드 서버와 통신하려면, 백엔드 서버의 주소도 HTTPS 인증을 받아야 한다.

abc.co.kr 을 구매 했으면 api.abc.co.kr 같이 앞에 어떠한걸 붙여도 사용할 수 있다.

## ELB를 활용한 아키텍처 구성

## ELB 셋팅하기 - 기본 구성

### IPv4와 IPv6의 차이
IPv4 주소는 일반적인 IP주소 123.12.0.5
IPv6는 IPv4의 고갈될 것을 예측하고 추가해 만들었다

## ELB 셋팅하기 - 보안그룹

## ELB 셋팅하기 - 리스너 및 라우팅/헬스 체크

### 상태 검사 (Health Check)

## ELB에 도메인 연결하기

## HTTPS 적용을 위해 인증서 발급받기

### Certificate Manager

## ELB에 HTTPS 설정하기

## 비용 나가지 않게 ELB 깔끔하게 종료하기

## HTTPS 연결 시 ELB vs Nginx, Certbot

현업에서는 ELB를 활용해서 HTTPS 적용을 더 많이 시킨다. 인증서의 만료기간 갱신도 자동으로 해준다.

Nginx와 Certbot을 활용해서 HTTPS를 적용시키는 가장 큰 이유는 **비용**

## Nginx, Certbot을 활용해 HTTPS 연결하기

### Certbot
HTTPS 인증서를 발급받아 주는 역할