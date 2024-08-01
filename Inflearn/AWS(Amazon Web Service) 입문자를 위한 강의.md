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