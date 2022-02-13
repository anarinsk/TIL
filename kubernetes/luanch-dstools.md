# Launching Data Science Tools 

## Why 

- docker-compose 대신 k8s를 써보자. 
- 딱히 실용적이진 않지만 재미 삼아 해보는 용도도 있다. 

## Conditions 

### Macos 

- Rancher desk을 쓰자. 
    + minikube를 써도 되는 듯 싶지만, 그래야 할 이유가 있을까? 
    + 어차피 minikube라는 게 데스트탑에서 k8s 그리고 CLI인 kubectl을 쓰게 해주는 용도이니까... 

### Windows 

- TBD 

## yaml 론칭 순서 

- 먼저 pod를 띄운다. 
    + pod는 jupyter와 rstudio 컨테이너를 지니고 있다. 
- pod를 띄울 때 local volume을 쉽게 마운트해줄 수 있다. 
    + 퍼시스턴트 볼륨(pv), 퍼시트턴트 볼륨 클레임(pvc)를 만들고 할 수도 있을 듯 하다... 
    + 일단 큰 문제가 없으니 편하게 가자. 

```shell
kubectl create -f dstools-pod.yaml 
kubectl create -f jupyter-service.yaml 
kubectl create -f rstudio-service.yaml 
```

- 컴마로 붙여서 연속으로 실행할 수 있다. 