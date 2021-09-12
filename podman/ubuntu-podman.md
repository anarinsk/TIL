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
podman run hello-world 
```

## nvidia container  

- [여기](https://github.com/anarinsk/til/blob/master/nvidia/nvidia-container.md#podman)를 참고하자. 

## docker-compose + podman

https://docs.docker.com/compose/install/#install-compose-on-linux-systems

- 도커 컴포즈를 설치하자. 

### docker_host to podman

https://stackoverflow.com/a/68142112

```shell
1$ systemctl --user start podman.socket
2$ export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/podman/podman.sock
```

1. systemctl 명령을 통해서 podman의 소켓을 개시하는 것이다. 소켓의 상태를 보고 싶다면, `start` &rarr; `status`
2. docker를 지웠으므로 이를 대신할 가상화 앱을 지정해야 한다. 이를 포드맨 소켓과 연결한다. 

- 이 상태에서 `docker-comppose`를 얹으면 잘 돌아간다. 
- 부팅 시 자동으로 준비가 되게 하려면 1,2를 .bashrc에 넣는다. 