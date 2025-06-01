### minikube 실행
[[minikube 실행]]
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

`helm install --dry-run --debug hands-on-dev-env kubernetes/helm/environments/dev-env`
- 렌더링된 매니페스트를 쿠버네티스 클러스터에 실제로 적용할 수 있는지 확인하는 커맨드
- `helm install`뒤에 `--dry-run` 플래그를 전달해 설치 테스트를 실행해볼수 있다.
- `--debug` 플래그를 전달하면 헬름이 매니페스트를 렌더링할 때 사용하는 사용자 제공 값과 계산 값도 표시한다.

`helm install hands-on-dev-env kubernetes/helm/environments/dev-env -n hands-on --create-namespace`
- hands-on 네임스페이스를 생성하고 전체 시스템 환경을 배포한다.

`helm uninstall hands-on-dev-env -n hands-on`
- 삭제 네임스페이스가 생성되어 있기 때문에 지우고 하지 않으면 실행되지 않음

`kubectl config set-context $(kubectl config current-context) --namespace=hands-on`
- 새로 생성한 네임스페이스를 kubectl의 기본 네임스페이스로 설정한다.

`kubectl get pods --watch`
- 포드 시작 과정을 볼수 있다.

`kubectl wait --timeout=600s --for=condition=ready pod --all`
- 네임스페이스의 모든 포드가 준비될 때까지 기다린다.

`kubectl describe pod mysql-747f8d8c78-mkjmh -n hands-on`
- Pod 상세 확인

`kubectl logs mysql-747f8d8c78-mkjmh -n hands-on`
- 로그 확인

`helm upgrade hands-on-dev-env ./kubernetes/helm/environments/dev-env -n hands-on`
- helm을 업그레이드 한다.
- values.yaml을 수정하는등을 하고 나서 그걸 업그레이드하고 업그레이드를 하면 version이 올라감
- `./kubernetes/helm/environments/dev-env`
	- 최종적으로 저장하는 느낌이 있어서 dev-env가 의존성 업데이트가 필요하면 하고 나서 봐야함

`helm get values hands-on-dev-env -n hands-on --all`
- 설정 확인

`kubectl get pods -o json | jq -r '.items[].spec.containers[] | .image'`
- 도커 이미지 확인

`kubectl get services -n hands-on`
- 열려있는 서비스 확인 커맨드