# How to make custom build with kaniko

## prereq

- kaniko는 google에서 개발한 빌드 툴로서 k8s kaniko를 끌어와서 이 녀석으로 빌드를 한다. 
- docker 혹은 별도의 빌드 툴이 필요 없다. 

## Why 

- Kaniko를 활용해서 dockerfile을 빌드해보자. 
- 나중에 네이티브 클라우드를 쓸 떄 필요하다. 

## How 

https://github.com/GoogleContainerTools/kaniko/blob/main/docs/tutorial.md

### 사전 작업 

- docker 관련한 주소 및 아이디/비밀번호 설정 
    + 크리덴셜로 활용한다. 

```
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=YOUR-ID --docker-password=YOUR-PASSWORD --docker-email=YOUR-EMAIL
```

### Volume 설정 

- 로컬 디스크와 연결하는 과정이다. 
- k8s의 특성상 volume과 volume-claim 두 개를 yaml로 설정해주자. 

### pod 띄우기 

- pod를 띄운다. 
- 하나의 pod 내에 container 여러 개를 설치할 수 있다. 


