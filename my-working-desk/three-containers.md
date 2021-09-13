# 컨테이너 삼총사 설정을 빠르게 따라가 보자. 

## Why 

- 자주 쓰는 환경인데 자주 까먹는다.

## Component 

- Jupyter Data Science 
- RStudio + Tidyverse 
- Tensorflow + Jupyter 

## WSL-Ubutu vs Ubuntu native 

- 둘 간에 비교를 해보자. Ubuntu native를 기본으로 두었을 때 아래와 같다. 

|설치 항목|WSL-Ubuntu|기타|
|------|:---:|----|
|podman|Ubuntu와 동일|
|nvidia container|Ubuntu와 동일|
|docker-compose|systemd 설정 필요|

- 별로 큰 차이가 없다. docker-compose를 구동하기 위해서 systemd 설정만 풀어주면 된다. 

## WSL-Ubuntu

### prerequisite 

https://github.com/anarinsk/setup-wsl-daily_use

- wsl 2를 쓸 수 있는 기본 환경 

### To-do list 

- podman 설치 
- docker-compose를 쓰기 위한 설정 및 docker-compose 설치 
- nvidia container toolkit 
- container image setups 

### Podman 설치 

https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md#installation

- 별도의 환경설정이 꼭 필요한지는 모르겠다... 

### docker-compose 이슈 해결 

https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md#with-docker-compose

- wsl 2에서 systemd를 지원하지 않기 때문에 번거로운 절차를 거쳐야 한다. 

#### 시나리오 

- systemd를 쓸 수 있도록 필요한 런타임, genie 설치 
- wsl 가동을 `wsl genie -s` 여기서 `-s`는 shell을 뜻한다. 
- docker-composer 설치 

### nvidia-container-toolkit 

https://github.com/anarinsk/til/blob/master/nvidia/nvidia-container.md#podman

- docker에는 gpu 옵션이 있다. 이를 통해 도커에서 엔디비아의 GPU 옵션은 활용할 수 있는데, podman에서는 해당 옵션을 받지 못한다. 
- 이를 해결하기 위해서 nvidia-container toolkit을 통해서 podman에서도 GPU를 부릴 수 있도록 만들 수 있다. 

### container image setups 

https://github.com/anarinsk/setup-docker_compose

- 여기서부터는 docker-compose의 활용과 동일하다. 

