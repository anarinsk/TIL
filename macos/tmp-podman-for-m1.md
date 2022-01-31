# Podman for M1 

## Why 

- Docker Desktop 후지다. 
- 포드맨을 써보자. 
- docker-compose와는 연동이 되어야 한다. 

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

## Problem of `docker-compose`

- docker-compose를 오리지널대로 쓰기 위해서는 vm안에 소켓을 열어줘야 한다. 
- 순서는 다음과 같다. 
    + vm에 진입 
    + vm에서 소켓을 열어주기 
    + https://fedoramagazine.org/use-docker-compose-with-podman-to-orchestrate-containers-on-fedora/
- vm을 설치했을 때 한번만 열어주면 되는 것 같다. 

```shell
[macos]
> podman machine ssh
[vm]
> sudo systemctl enable podman.socket
> sudo systemctl start podman.socket
> sudo systemctl status podman.socket 
```

- 소켓에 불이 들어 와 있으면 잘 활성화된 것이다. 

- 확인하는 스크립트는 아래와 같다. 

```shell
sudo curl -H "Content-Type: application/json" --unix-socket /var/run/docker.sock http://localhost/_ping
```

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