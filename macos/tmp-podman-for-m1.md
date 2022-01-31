# Podman for M1 

## Why 

- Docker Desktop 후지다. 
- 포드맨을 써보자. 
- docker-compose와는 연동이 되어야 한다. 

## tl; dr 

- brew를 통해서 podman, docker-compose 설치 
- `podman machine ssh`로 vm에 진입해서 소켓 활성화해주기 

## tbd 

- podman 명렁어 셋 만들어 두기 

## Install

- brew에서 인스톨 하자. 
    + brew 검색 창에서 'podman', 'docker-compose' 검색 
- 참고 
    + https://www.redhat.com/sysadmin/replace-docker-podman-macos

### podman 

- vm 활성화해주자. 
    + https://podman.io/getting-started/installation
    
    ```shell
    podman machine init
    podman machine start
    ```

    + `podman run --rm hello-world`로 테스트 해보자. 

## Be practical 

- podman mac은 podman이 먼저 Fedora 기반 vm을 설치하고 이 녀석 안에 podman을 깔아서 운용한다. 
- 같은 기술로 운용되기 때문에 기술적인 제약은 크지 않은 듯 싶다... 

- 아래 스크립트가 vm을 실행하는 스크립트다. 

```shell
podman machine init 
podman machine start 
```

## Problem of docker-compose

- 아래 가이드가 완벽하다. 
https://blog.bassemdy.com/2021/11/06/containers/oci/docker/podman/docker-compose/podman-and-docker-compose-on-macos.html

### 주의사항 

그냥 복붙은 곤란하니, 다래의 두 포인트를 주의하자. 

- host machine의 ssh를 설치할 때 

<PODMAN_MACHINE_NAME>

```
export DOCKER_HOST="ssh://root@localhost:<PORT>"
```

<PORT>

### 어이 없는 대목 

- docker-compose 실행할 때 이상한 에러가 뜰 수 있다. 

```
In ~/.docker/config.json change credsStore to credStore
```

- 한마디로 실행 변수에 오타가 있다. 이걸 고쳐주자. 


## Unistall 

### Docker-desktop 

-  안에 troubleshooting
    + purge data 
    + uninstall 
- OS에 남아 있는 관련 데이터 지우기 
    + 안 해도 되는 듯 싶다. 
    + https://www.mytecbits.com/apple/macos/clean-way-to-uninstall-docker

### Podman 

- 먼저 vm을 날려야 한다. 
- 그리고 brew로 언인스톨하자. 

```
podman machine rm podman-machine-default
brew uninstall podman
```