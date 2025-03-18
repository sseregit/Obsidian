# 1. 강의 소개
## 강의 소개

****
# 2. MySQL 설치 및 실행 환경 구성하기
## [[환경 구성을 위한 CLI 명령어 리스트 입니다.]]

## EC2 생성 및 Linux 권한 설정 다루기
`-rw-r--r--@   1 yeonsigjang  staff       1674  3 18 14:28 ****.pem`
### `-rw-r--r--`
- 첫번째 -
	- `-`: 파일
	- `d`: 폴더
- 그후 3자리씩
	- r
		- read
	- w
		- write
	- e
		- exception
	- 처음 3자리
		- 파일에 대한 소유자
	- 두번째 3자리
		- 소유자 그룹의 권한
		- 소유자는 반드시 그룹에 속해있다.
	- 마지막 3자리
		- 기타 사용자에 대한 권한
### `chmod <소유자/그룹/전체> <파일>`
- r: 4
- w: 2
- e: 1
`chmod 400 ****.pem`
- 소유자는 read, 그룹, 전체는 아무 권한도 주지 않는다.
## Password 기반의 접속 설정을 위한 ssh 환경 변수 다루기
### `sshd_config`파일
- ssh 접속에 대해서 제어를 하는 파일
****
# 3. MySQL Security
## MySQL 설치 및 GPG 에러 디버깅 하는법
[[GPG?]]
## MySQL 최초 설치에 따른 접근 제어하기
## MySQL 초기 비밀번호 추출 및 변경하기
## MySQL Security를 위한 권한 제어하기
****
# 4. Module Skelton
## 소스코드 및 총 데이터 csv 파일 입니다.
## Migration 작업 목표
## 유연한 환경변수 관리하기
[[*.toml?]]
## DB 접속 정보 전달하기
## 일반적인 Migration Module 구성
****
# 5. DB Optimize & Service Logic
## 공공데이터 추출을 위한 로직 작성하기
## Google Geocoding API를 활용한 로직 작성하기
## Google Geocoding API Response 분석하기
## DB Insert 최적화
## MySQL Insert Optimization

****
# 6. Test 및 강의에 대한 추가적인 정보

****