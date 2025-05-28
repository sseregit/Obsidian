`minikube start`
- minikube가 실행되어 있어야함
### 도커 이미지 빌드
`eval $(minikube docker-env)`
- 커맨드를 실행하고 도커 이미지를 빌드하면 미니큐브의 도커 엔진과 도커 클라이언트가 통신하게 된다.
- 내부적으로 환경설정이 minikube 안의 docker 엔진으로 바라본다.
- 일회용 사용할 때마다 설정해줘야한다.
-  `./gradlew build && docker compose build`
	- 이미지가 minikube 내부의 docker 엔진에 저장됨
### 헬름 차트의 의존성 해결
`for f in kubernetes/helm/components/*; do helm dep up $f; done`
- components 폴더의 helm 차트의 의존성을 해결
`for f in kubernetes/helm/environments/*; do helm dep up $f; done`
- environments 폴더의 helm 차트의 의존성을 해결
`helm dep ls kubernetes/helm/environments/dev-env/`
- dev-env 폴더의 의존성을 확인한다.

### 쿠버네티스에 배포
**이미 이미지가 있어서 스킵했지만 필요한 이미지들은 미리 받아두는것이 좋다. 이미지 다운로드가 지체되면 라이브니스 프로브가 포드를 재시작할 우려가 존재**

`helm template kubernetes/helm/environments/dev-env`
- 헬름 차트를 사용하기전 `helm template` 커맨드를 사용해 템플릿을 렌더링해 생성될 매니페스트를 확인
- 쿠버네티스 클러스터와 연동해 렌더링한것은 아니므로 가상의 클러스터 정보가 나타나고 렌더링된 매니페스트를 클러스터에 적용할 수 있는지 확인하는 테스트도 실행되지 않는다는 점에 유의


