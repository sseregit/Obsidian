```bash
unset KUBECONFIG

minikube start \
--profile=handson-spring-boot-cloud \
--memory=10240 \
--cpus=4 \
--disk-size=30g \
--kubernetes-version=v1.33.1
--driver=docker

minikube profile handson-spring-boot-cloud

minikube addons enable ingress --profile=handson-spring-boot-cloud
minikube addons enable metrics-server --profile=handson-spring-boot-cloud
```