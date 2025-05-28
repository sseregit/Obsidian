```bash
unset KUBECONFIG

minikube start \
--profile=handson-spring-boot-cloud \
--memory=9000 \
--cpus=4 \
--disk-size=30g \
--kubernetes-version=v1.33.1 \
--driver=docker

minikube profile handson-spring-boot-cloud

minikube addons enable ingress --profile=handson-spring-boot-cloud
minikube addons enable metrics-server --profile=handson-spring-boot-cloud
```

- Docker Desktop이 제공할 수 있는 최대 메모리가 9,951MB이 이상이면 오류
	- 이건 Docker Desktop의 Resources의 Memory의 설정 때문으로 보인다.

`minikube stop`
- 쿠버네티스 클러스터 중지

`minikube start`
- 다시 쿠버네티스 클러스터 시작

`minikube delete --profile handson-spring-boot-cloud`
- 프로필을 지정하지 않아도 되지만 명시적으로 지정하는것이 안전하다.