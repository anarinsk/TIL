# Launching Data Science Tools 

## Cross reference 

[TIL: k8s yaml]()

## Why 

- docker-compose 대신 k8s를 써보자. 
- 딱히 실용적이진 않지만 재미 삼아 해보는 용도도 있다. 

## Conditions 

### Image is built 

- dockerhub : https://hub.docker.com/repositories
    + 아래 두 개의 리포를 참고하자. 
    + rstudio-m1-korfont 
    + jupyter-ds-korfont 

### Macos 

- Rancher desk을 쓰자. 
    + minikube를 써도 되는 듯 싶지만, 그래야 할 이유가 있을까? 
    + 어차피 minikube라는 게 데스트탑에서 k8s 그리고 CLI인 kubectl을 쓰게 해주는 용도이니까... 

### Windows 

- TBD 

## yaml 론칭 순서 

- example: https://github.com/anarinsk/setup_k8s/tree/main/dstools-deployment

- 먼저 pod를 띄운다. 
    + pod는 jupyter와 rstudio 컨테이너를 지니고 있다. 
- pod를 띄울 때 local volume을 쉽게 마운트해 줄 수 있다. 
    + 퍼시스턴트 볼륨(pv), 퍼시트턴트 볼륨 클레임(pvc)를 만들고 할 수도 있을 듯 하다... 
    + 일단 큰 문제가 없으니 편하게 가자. 

```shell
kubectl create -f dstools-pod.yaml 
kubectl create -f jupyter-service.yaml 
kubectl create -f rstudio-service.yaml 
```

- 컴마로 붙여서 연속으로 실행할 수 있다. 

## YAML 해설 

https://github.com/anarinsk/setup_k8s/blob/main/dstools-deployment/dstools-pod.yaml

### Pod related 

- 파드를 띄우는 yaml이다. 
- 구조의 위계는 다음과 같다. 

#### H1 
- `apiVersion` 
- `kind`
- `metadata`
- `spec` 

- 제일 중요한 것은 `spec`이다. 

#### spec 

- `containers` 
    + 컨테이너 관련 정보 
    + docker-compose 설정을 거의 가져다 쓰면 된다. 
    + `volumeMounts`가 중요 
- `volumeMounts`
    + `name`: 아래 `volumes`에서 설정한 이름을 가져다 쓴다. 
    + `mountPath`: 컨테이너 내에 연결될 패스를 설정한다. 도커에서 `:`의 우변이다. 
- `volumes`
    + `name`: 볼륨의 이름을 설정한다. 
    + `hostPath`: 호스트의 패스를 설정한다. 로컬의 디렉토리를  OS에 맞춰서 설정하자. 

###  Service related 

https://github.com/anarinsk/setup_k8s/blob/main/dstools-deployment/jupyter-service.yaml

- `nodePort` 설정으로 포트를 맞춰주자.
- `selector` 항목에서  `app: jupyter-rstudio` 식으로 pod의 app 이름과 맞춰주어야 한다.  
    + 그렇지 않으면 service가 pod를 찾아가지 못한다. 


