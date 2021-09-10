# Podman in WSL 2 

- Docker Desktop 유료화되서 쓴다!  

## Installation 

- 어차피 WSL 2에서 밖에 안 쓰게 되지 않을까 싶다. 
- podman의 모든 명령어는 docker와 호환된다. 따라서 podman 자체로 바꾸는 데에는 큰 문제가 없다. 
- podman >= 3.0 이상 부터 설치가 간편하다. 

기본적으로 [여기](https://wbhegedus.me/running-podman-on-wsl2/) 가이드가 완벽하다. 다만 진행 순서가 틀렸다. 

```shell
1> cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

2> export VERSION_ID="20.04"

> echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
> curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/Release.key | sudo apt-key add -
> sudo apt-get update
> sudo apt-get -y upgrade
> sudo apt-get -y install podman
```

1. Ubuntu의 버전을 확인한다. 
2. `VERSION_ID` 항목의 버전을 확인해서 넣어준다. 
- 이후는 포드맨을 설치하는 절차다. 

## ENV 

- 환경 설정을 위해서 아래의 두 작업을 한다. 
    + `~/.config/containers` 디렉토리를 만든다. 
    + `~/.config/containers/containers.conf` 파일을 생성한다. 

```shell
$ mkdir -p ~/.config/containers
$ sudo nano ~/.config/containers/containers.conf
```

```shell
[engine]
events_logger="file"
cgroup_manager="cgroupfs"
```

- 위의 내용을 넣어주고 저장한 후 재 부팅

## With `docker-compose`

- 도커 컴포즈와 쓰기 위해서는 조금 복잡하다. systemd를 설정해주는 과정이 필요하기 때문이다. 이를 위해서 ginie를 설치해야 한다. 
- 기본 절차는 [여기](https://github.com/arkane-systems/genie)를 참고하자. 

가이드에 있는 대로 

### 사전 설치 

- [.net 런타임 설치](https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu)
- [wsl-transdevian 설치](https://arkane-systems.github.io/wsl-transdebian/)
    + lsb_release를 먼저 설치하자. `apt-get install lsb`
    + 아래 스크립트를 `sudo -s` 상태에서 실행한다. 

```shell
wget -O /etc/apt/trusted.gpg.d/wsl-transdebian.gpg https://arkane-systems.github.io/wsl-transdebian/apt/wsl-transdebian.gpg

chmod a+r /etc/apt/trusted.gpg.d/wsl-transdebian.gpg


cat << EOF > /etc/apt/sources.list.d/wsl-transdebian.list
deb https://arkane-systems.github.io/wsl-transdebian/apt/ $(lsb_release -cs) main
deb-src https://arkane-systems.github.io/wsl-transdebian/apt/ $(lsb_release -cs) main
EOF
apt update
```

### Genie & docker-compose 

```shell
$ sudo apt update
$ sudo apt install -y systemd-genie
```

- docker-compose 설치 `apt-get install docker-compose`

## To run docker-compose with podman 

- 포드맨에서 docker-compose를 실행하기 위해서는 우선 systemd가 활성화되어야 한다. 이를 위해서 Powershell에서 다음과 같이 실행하자. 

```shell
> wsl genie -s
```

- 가끔 대기가 걸릴 떄가 있는데 무시하고 다시 실행해주면 대개 잘 된다. 
- 이제 이 상태에서 두 개의 일을 해준다. 

```shell
1$ systemctl --user start podman.socket
2$ export DOCKER_HOST=unix://$XDG_RUNTIME_DIR/podman/podman.sock
```

1. systemctl 명령을 통해서 podman의 소켓을 개시하는 것이다. 소켓의 상태를 보고 싶다면, `start` &rarr; `status`
2. docker를 지웠으므로 이를 대신할 가상화 앱을 지정해야 한다. 이를 포드맨 소켓과 연결한다. 

- 이 상태에서 `docker-comppose`를 얹으면 잘 돌아간다. 

- WSL 부팅 시 자동으로 준비가 되게 하려면 1,2를 .bashrc에 넣는다. 
    + 단 `wsl genie -s` 상태가 아니라면 systemd 사용이 제한되기 때문에 경고 메시지를 볼 수 있다.  
    + `Failed to connect to bus: No such file or directory`

## Problem left 

- 이전 docker dssktop에서와 같은 편리한 VS Code 접속은 한동안 기다려야 할 것 같다. 
