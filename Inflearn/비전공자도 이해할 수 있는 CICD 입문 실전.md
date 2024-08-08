## [수업자료](https://jscode.notion.site/a296752baf914e8ab95a1782a64800c2)

## CI/CD를 왜 배우는 걸까?

### CI/CD란?
테스트(Test), 통합(Merge), 배포(Deploy)의 과정을 자동화하는 걸 의미한다.

## CI/CD 구축할 때 사용할 Github Actions

### CI/CD 구축할 수 있는 툴
- Github Actions
- Jenkins
- Circle CI
- Travis CI
- 등등..

## Github Actions를 활용한 전체적인 CI/CD 흐름

### Github Actions
로직을 실행시킬 수 있는 일종의 컴퓨터

일반적인 흐름
commit -> push -> push를 감지해서 Github Actions에 작성한 로직이 실행
1. 빌드(Build)
2. 테스트(Test)
3. 서버로 배포(Deploy)
 서버에서 배포된 최신 코드로 서버를 재실행

## [실습] Github Actions 기본 문법 정리

프로젝트 최상단에 .github 폴더와 그안에 workflows가 존재해야 한다
그 이후 yml파일의 이름은 자유롭게

WorkFlow는 여러 Job으로 구성 되어 있고
Job은 기본적으로 병렬적으로 수행된다.

Job은 여러 Step들로 구성되어 있다.
Step은 특정 작접을 수행하는 가장 작은 단위