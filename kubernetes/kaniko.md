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
- yaml 파일이 있는 로컬 디렉토리에서 실행한다고 가정하자. 

- `volume.yaml` 파일 내부에 마운트되는 로컬 디렉토리에 주의하자. os별로 다를 수 있다. 

```shell
kubectl -f volume.yaml 
kubectl -f volume-claim.yaml 
```

### pod 띄우기 

- pod를 띄운다. 
- 하나의 pod 내에 container 여러 개를 설치할 수 있다. 
    + container 별로 별도의 툴을 빌드할 수 있다! 
    + 내 경우는 rstudio와 jupyter를 각각 빌드한다. 

- `kubectl -f pod.yaml`

- 제대로 실행되면 pod가 올라가면서 이미지를 빌드해서 dockerhub의 개인 저장소로 빌드된 이미지를 보낸다. 

### Trouble shooting 

- `kubectl get all`
    + 파드 및 다른 정보 보기 
- `kubectl get pv`
    + 퍼시트턴트 볼륨 보기 
- `kubectl get pvc`
    + 퍼시트턴트 볼륨 클레임 보기 
- `kubectl delete pod/kaniko`
    + 파드 삭제 
- 퍼시스턴트 볼륨 역시 같은 방식으로 지울 수 있다. 
    + 단 문제가 생겼을 경우에는 리셋이 필요하다. (파일 참고)
- `kubectl describe pod/kaniko`
    + 파드 생성의 진행 상황을 파악할 수 있다. 
- `kubectl logs pod/kaniko build-jupyter`
    + 컨테이너 빌드의 진행상황을 보여준다. 

## Working examples 

- https://github.com/anarinsk/setup_k8s/tree/main/build-tools/kaniko





