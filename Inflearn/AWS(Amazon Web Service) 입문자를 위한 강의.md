## 환영합니다

## AWS 계정 만들기
### As You Pay Go 서비스
### Free-tier 서비스
### 루트(Root) 사용자

## IAM이란?

### IAM (Identity and Access Management)
유저를 관리하고 접근 레벨 및 권한에 대한 관리

- 접근키(Access key), 비밀키(Secret Access key)
- 매우 세밀한 접근 권한 부여 가능 (Granular Permission)
- 비밀번호를 수시로 변경 가능케 해줌
- Multi-Factor Authentication(다중 인증) 기능

- 그룹 (Group)
- 유저 (User)
- 역할 (Role)
- 정책 (Policy)
	- 주로 JSON형태의 Document

- 정책은 그룹, 역할에 추가 시킬 수 있다
- 하나의 그룹 안에 다수의 유저가 존재 가능하다

IAM은 유니버설(Universal) 하다
- 지역 설정이 필요 없음

## IAM 정책 시뮬레이터
1. 개발환경(Staging or Develop)에서 실제환경(Production)으로 빌드하기전 IAM 정책이 잘 작동되는지 테스트하기 위함
2. IAM과 관련된 문제들을 디버깅하기에 최적화된 **툴**(이미 실제로 유저에 부여된 다양한 정책들도 테스트 가능)

## IAM 실습하기

## EC2란?

### EC2 (Elastic Compute Cloud)

### 다양한 지불 방법
- On-demand
	- 시간 단위로 가격이 고정되어 있다.
- Reserved
	- 한정된 EC2 용량 사용 가능
	- 1 ~ 3년 동안 시간별로 할인 적용 받을 수 있다.
	- On-demand와 달리 조금더 저렴하고 크기를 늘리고 줄일 수 없다
	- 사이즈를 정해야 한다
- Spot
	- 입찰 가격 적용
	- 가장 큰 할인율을 적용받으며 특히 인스턴스의 시작과 끝기간이 전혀 중요하지 않을때 매우 유용

### 사용 용례
- On-demand
	- 오랜시간동안 선불을 내지 않고 최소한의 비용을 지불하여 EC2인스턴스를 사용하고 싶을 때
	- 개발기간이 정확하지 않을 때 사용하기 좋다 or 개발 초기 단계
- Reserved
	- 예상 가능한 workload시 Reserved 사용 권장, 선불로 인한 컴퓨팅 비용 대푝 감소
	- 개발기간이 예측 가능할 시 사용한다
- Spot
	- 단순히 비용 절감 시 유용하다
	- 인스턴스의 시작/끝시점에 구애받지 않을 경우 권장

### EBS
EC2안에 부착된 하드디스크라 생각하면 쉽다.

## EBS

### EBS
- 저장 공간이 생성되어 지며 EC2 인스턴스에 부착된다
- 디스크 볼륨 위에 File System이 생성된다
- EBS는 특정 Availability Zone에 생성된다.

### Availability Zone (AZ)
- 하나의 Region안에 여러개의 AZ가 있을 수 있다.
- 일종의 Disaster Recovery

### EBS 볼륨 타입
#### SSD군
- General Purpose SSD (GP2)
	- 최대 10K IOPS를 지원하며 1GB당 3IOPS 속도가 나온다
- Provisioned IOPS SSD (IO1)
	- 극도의 I/O률을 요구하는 (매우 큰 DB관리 등등..) 환경에서 주로 사용된다.
	- 10K 이상의 IOPS를 지원한다
#### Magnetic/HDD군
- Throughput Optimized HDD (ST1)
	- 빅데이터 Datawarehouse, Log 프로세싱시 주로 사용 (boot volumne으로 사용 불가능)
- CDD HDD (SC1)
	- 파일 서버와 같이 드문 volume 접근시 주로 사용, 역시 boot volume으로 사용 불가능하나 비용은 매우 저렴하다
- Magnetic (Sandard)
	- 디스크 1GB당 가장 싼 비용을 자랑하고 Boot volume으로 유일하게 가능하다
**boot volume 사용불가능은 window같은걸 가지고 있을수 없다 같은 의미**

## ELB

### ELB (Elastic Load Balancers)
- 수 많은 서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 한다
- 하나의 서버로 traffic이 몰리는 병목현상(bottleneck) 방지
- Traffic의 흐름을 Unhealthy instance -> healthy instance로

#### Application Load Balancer
- OSI Layer7에서 Application Layer에서 작동된다
- HTTP, HTTPS와 같은 traffic의 load balancing에 가장 적합하다
- 고급 request 라우팅 설정을 통하여 특정 서버로 request를 보낼 수 있다

#### Network Load Balancer
- OSI Layer4 에서 작동 된다
- 매우 빠른 속도를 자랑하며 Production환경에서 종종 쓰인다
- 극도의 performance가 요구되는 TCP traffic에서 적합하다
- 초당 수백만개의 request를 아주 미세한 delay로 처리 가능하다

#### Classic Load Balancer
- 현재 Legacy로 간주되고 거의 사용되지 않는다
- Layer7의 HTTP/HTTPS 라우팅 기능 지원
- Layer4의 TCP traffic 라우팅 기능도 지원

#### X-Forwarded-For 헤더