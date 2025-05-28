`minikube start`
- minikube가 실행되어 있어야함
### 도커 이미지 빌드
`eval $(minikube docker-env)`
- 커맨드를 실행하고 도커 이미지를 빌드하면 미니큐브의 도커 엔진과 도커 클라이언트가 통신하게 된다.
- 내부적으로 환경설정이 minikube 안의 docker 엔진으로 바라본다.
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

