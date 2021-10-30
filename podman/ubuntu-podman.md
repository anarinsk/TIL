# ubuntu에 podman을 설치해보자. 

## Why 

- docker 재수 없어서 못 쓰겠다! 
- podman을 ubuntu에 설치하고, nvidia gpu 연동까지 해결해보자. 

## Installation 

https://podman.io/getting-started/installation

- 링크의 ubuntu 부분을 참고하자. 
- 아래 코드로 실행하면 된다. 이 과정은 wsl 2와 동일하다. 

```shell
1$ cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

2$ export VERSION_ID="20.04"

$ echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
$ curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/Release.key | sudo apt-key add -
$ sudo apt-get update
$ sudo apt-get -y upgrade
$ sudo apt-get -y install podman
```

1. 설치된 우분투 버전을 확인하자. 
2. 해당 버전을 설정한다. 

### Testing 

- docker의 hello-world를 실행해보자. 

```shell
podman run --rm hello-world 
```

## nvidia container  

- [여기](https://github.com/anarinsk/til/blob/master/nvidia/nvidia-container.md#podman)를 참고하자. 

## docker-compose + podman

- 이하의 과정은 WSL 2와 거의 동일하다. 

```shell
sudo apt-get update 
sudo apt-get install docker-compose 
```

- 공식 가이드대로 설치하니 에러가 나더라. 뭔가 빼먹은 듯.   
    + https://docs.docker.com/compose/install/#install-compose-on-linux-systems

### docker_host to podman

https://stackoverflow.com/a/68142112

```shell
1$ systemctl --user start podman.socket
2$ export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/podman/podman.sock
```

1. systemctl 명령을 통해서 podman의 소켓을 개시하는 것이다. 소켓의 상태를 보고 싶다면, `start` &rarr; `status` 바꿔서 실행한다. 
2. docker를 지웠으므로 이를 대신할 가상화 앱을 지정해야 한다. 이를 포드맨 소켓과 연결한다. 

- 이 상태에서 docker-compose를 얹으면 잘 돌아간다. 
- 부팅 시 자동으로 준비가 되게 하려면 1,2를 .bashrc에 넣는다. 
    + wsl에서와 달리 `.bashrc`에 넣어도 큰 문제가 생기지 않는다. 

### Checkpoints 

- `sudo` 없이 실행해야 한다. 
    + local directory를 마운트할 때 많은 애로 사항이 있다. 
- VS Code 콘테이너 접속도 무리 없이 잘 된다. 
    + settings.json에서 Docker Path를 바꾸지 않아도 된다. 
    + 아마도 docker-compose를 깔았기 때문인 듯... 

### Rocker 컨테이너 이미지 권한 문제 

#### dockerfile 

- container 계정이 rstudio를 쓰고 있다고 가정하자. 
- container가 시작해서 volume이 마운트될 때 기본으로 root와 된다. 
- 따라서 rstudio를 root group안에 넣어야 마운트된 폴더에서 작업이 가능하다. 
- dockerfile `RUN` 항목에 아래와 같이 삽입하자. 

```shell
&& usermod -G root rstudio 
```

- 명령어 해설 
    + `usermod`: 계정을 특정한 그룹이 넣는다. 
    + `-G`: 주 그룹을 그대로 두고 계정을 부 그룹에 넣는 옵션 
    + `root`: 계정을 넣을 그룹
    + `rstudio`: 대상 계정 

#### yml part 

- 단순한 권한 문제가 아니다. 이게 해결이 안되면 project와 renv를 제대로 쓸 수 없다. 
- WSL을 활용할 때는 yml에 아래와 같이 enviroment를 설정한다. 

```shell
volumes: 
            - /mnt/e/github:/home/rstudio/github-anari
            - /mnt/e/renv:/home/rstudio/renv
        ports: 
            - "8787:8787"
        environment: 
            - PASSWORD=1022
            - UMASK=000
            - ROOT=TRUE
            - RENV_PATHS_CACHE=/home/rstudio/renv
```

- volume의 두 번째 부분은 renv 환경에서 패키지 파일을 물리적으로 host에 저정하기 위한 것이다. 
- `UMASK=000`이다. 생성되는 폴더의 권한을 바꿔주는 부분이다. 
    + 이 옵션을 설정하지 않을 경우 Rstudio 컨테이너에서 생성한 폴더가 잠기게 되고, Ubuntu의 계정 home 파일에서는 수정할 수 없게 된다. 
    + `.Rprofile` 아래 `Sys.umask(mode=000)`으로 설정된다. dockerfile에서 해당 파일을 심어줘도 무방하다. 
