# Alternative to Docker Desktop 

## Why 

- 유료화 정책 
- 느린 퍼포먼스 

## Docker Desktop 

- m1에서 full package를 제공한다. 
- qemu를 백엔드로 쓰지만, 프론트엔드에서는 별다른 티가 나지 않는다. 

## Way 1: Rancher Desktop 

- 언제 유료화를 할지 모르지만, 일단은 좋다. 
- brew에서 설치하자. 

### 설치

`brew install --cask rancher`

### 설정

- 특별한 건 없었다. 
- 다만 최초 인스톨에서는 "Supporting Utilities"에서 docker 등이 활성화되지 않았다. 
    + 이유를 찾지 못함 

### 활용 

- 인스톨 후 docker 바로 활용 가능 
- docker-compose를 설치해주자. `brew install docker-compose`
- 콤포즈 명령어를 별다른 이슈 없이 쓸 수 있었다. 

### Ultimate Solution?

- Kubenetes로 전환을 해야 할 듯 싶다. 
- Minikube에 대해서 차츰 공부해가자. 

## Way 2: lima + docker + docker-compose 

### Resources 

https://breezymind.com/slicon-m1-mac-lima-docker-desktop-alternative/


### 설치

```
brew install lima docker docker-compose
```

### VM 올리기 

```
curl -o default.yaml https://raw.githubusercontent.com/lima-vm/lima/master/examples/docker.yaml
```

- ymal 파일을 다운로드 받는다. 
- `~` 폴더를 수정할 수 있게 고쳐준다. 

```
- location: "~"
  writable: true
```

- lima를 통해 vm을 설치한다. 

```
limactl start default.yaml 
```

- yaml 파일 이름을 꼭 "default"로 해야 하나? 
    + 그럴 필요는 없지만 그러는게 편리할 듯. 
    + default로 잡아 놓아야 "lima" 명령어를 편하게 쓸 수 있다. 

```
lima docker ps
```

- VM 내에게 도커가 제대로 설치되었는지 테스트해보자. 잘 되면 큰 문제 없는 것이다. 

### macos 설정 

- ssh 설정을 옮겨줘야 한다. 

```
limactl show-ssh --format=config default >> ~/.ssh/config
```

- `DOCKER_HOST를 설정해줘야 한다. 

```
export DOCKER_HOST=ssh://lima-default:60006
```

- 이 녀석은 `~/.zshrc`에 넣고 쓰도록 하자. 그래야 부팅시 매번 설정해주는 번거로움이 사라진다. 

### Practically 

- 리부팅한 후
  + 터미널에서 리마를 먼저 올리자. 
  + docker-compose 실행 

```shell
limactl start default 
docker-compose -f ~/Documents/GitHub/setup-docker_compose/MBP-M1/macos_podman_jupyter.yml -p "anari-ds" up -d
```
## Way 2-1: lima + docker + docker-compose 

- Host에 docker, docker-compose를 깔지 않는다. 
- guest에 이 모든 것을 깔고, yaml을 올리는 것으로 docker-image를 실행한다. 

```shell
limactl start 
lima docker-compose -f /Users/anari/Documents/GitHub/setup-docker_compose/MBP-M1/macos_podman_jupyter.yml -p "anari-ds" up -d
```

- 이미 default가 설정되어 있다면, limactl... 만으로 컨테이너를 다시 구동할 수 있다. 
- `lima` 내부에서 명령 실행
- lima 내부에 host의 /Users/anari, 즉 `$HOME` 폴더가 마운트돠어 있다. 따라서 해당 yml을 바로 돌릴 수 있다. 
