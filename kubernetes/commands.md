# commands 

-kubectl 명령어 자꾸 까먹어서 적어본다. 

## 조회 

- `kubectl get --all`: 파드와 서비스 모두 보기 
- `kubectl get pods`: 파드 보기 
- `kubectl describe pods {NAME-OF-POD}`: 파드 상세하게 보기 
- `kubectl logs {NAME-OF-POD} {NAME-OF-CONTAINER}`: 콘테이너 내부 프로세스 보기 

### Real examples 

- based on https://github.com/anarinsk/setup_k8s

```shell
kubectl get --all
kubectl get pods 
kubectl describe pods dstools 
kubectl logs dstools jupyter 
```

## 파드 생성 

- yaml 파일이 있는 디렉토리로 이동 
- `kubectl create -f {NAME-OF-FILE}`
