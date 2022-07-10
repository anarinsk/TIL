# nerdctl 

## Why 

- 도커에서 기본으로 돌리는 컨테이너 런타임이다. 
- 원래 ctr이라는 이름의 명령어이냐, 이 녀석은 사람과 친하지 않다. 
- 그래서 사람과 친한 버전인 nerdctl이 나오게 된 것이다. 

## 특징 

- 도커의 모든 기능과 명령어를 그대로 제공한다. 
    + compose도 제공해서 docker-compose도 따로 설치할 필요가 없다. 

### OS 

- Windows에서는 정신건강을 위해서 [rancher desktop](https://rancherdesktop.io/)을 쓰도록 하자. 
    + WSL 2와 잘 호환된다. 
- Macos에서는 [lima](https://github.com/lima-vm/lima)에 기본 탑재가 되어 있으며, m1(arm64)에서도 잘 돌아간다. brew로 설치하자. 
- [ ] Not tested in Ubuntu 

##  Quick examples 

- 빠르게 텍스트로 땡겨올 수 있는 테스트 

```shell
nerdctl run --rm hello-world
```
- 가짜 웹 & 포트포워딩 

```shell
nerdctl run --name mattermost-preview -d --publish 8065:8065 mattermost/mattermost-preview
```

- DS container 

```
nerdctl run -it --rm -v $PWD:/home/jovyan/work -u root -e JUPYTER_TOKEN=1022 -e GRANT_SUDO=yes -p 10000:8888 jupyter/datascience-notebook:aarch64-latest
```

## 실제 운용 

[setup_netcrl](https://github.com/anarinsk/setup_nerdctl)를 참고하자. compose 기반 실전 파일들이 . 

## Unsolved 

- [ ] RStdio 안 돌아간다. amd64, arm64 마찬가지 

```shell
nerdctl run -d -p 8787:8787 -e PASSWORD=1234 tazovsky/rstudio-m1:R-4.1.2
nerdctl run -d -p 8787:8787 -e PASSWORD=1234 tschaffter/rstudio:latest
nerdctl run -d -p 8787:8787 -e PASSWORD=1234 rocker/rstudio:lasest
```

### ad-hoc solution 

- 결국 docker를 쓸 수 밖에 없지 않은가...
    + podman도 가능하지만 docker-compose를 잘 쓸 수 없다. 
- docker를 쓰는 방법 
    + lima에 docker를 깔아서 context로 연결해서 쓴다. 
    + https://itnext.io/replace-docker-desktop-with-lima-88ec6f9d6a19 거의 완벽한 가이드 

#### My use case 
    + https://github.com/anarinsk/setup-docker_compose/tree/main/MBP-M1
    + 여기서 yml 및 도커 파일을 마련해 두었다. 
    + 빠르게 확인해보는 법: `docker run -d -p 8787:8787 -e PASSWORD=1234 tazovsky/rstudio-m1:R-4.1.2` 
