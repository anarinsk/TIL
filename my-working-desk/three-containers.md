# 컨테이너 삼총사 설정을 빠르게 따라가 보자. 

## Why 

- 자주 쓰는 환경인데 자주 까먹는다.

## Component 

- Jupyter Data Science 
- RStudio + Tidyverse 
- Tensorflow + Jupyter 

## WSL-Ubutu vs Ubuntu native 

- 둘 간에 비교를 해보는 게 의미가 있을 듯 싶다. 

|제목|내용|설명|
|------|---|---|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|


## WSL-Ubuntu

### prerequisite 

https://github.com/anarinsk/setup-wsl-daily_use

- wsl 2를 쓸 수 있는 기본 환경 

### To-do list 

- podman 설치 
- docker-compose를 쓰기 위한 설정 및 docker-compose 설치 
- container image setups 

### Podman 설치 

https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md#installation

- 별도의 환경설정이 꼭 필요한지는 모르겠다... 

### docker-compose 이슈 해결 

https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md#with-docker-compose

- wsl 2에서 systemd를 지원하지 않기 때문에 번거로운 절차를 거쳐야 한다. 

#### 개요 

- systemd를 쓸 수 있도록 필요한 런타임, genie 설치 
- wsl 가동을 `wsl genie -s` 여기서 `-s`는 shell을 뜻한다. 
- docker-composer 설치 

### container image setups 

- 여기서부터는 docker와 동일하다. 
