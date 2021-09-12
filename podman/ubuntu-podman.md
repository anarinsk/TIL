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

## nvidia docker 

- 여기부터 설정과정은 Wsl 2와 동일하다. 