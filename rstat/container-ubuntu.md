# Ubuntu에서 활용

## Problem 

- wsl 2 + podman의 rootless 환경 
- project로 잡히지 않은 상태에서는 아무 문제 없음 
- project가 설정된 상태에서 renv가 활성화되면 패키지 인스톨에 전체적으로 문제가 생긴다. 
    - xml2 패키지 설치에 문제 

## First thing first 

- renv를 위한 cache 환경을 docker-compose 내에서 설정해준다. 
- environment에서 `RENV...`를 설정하고, volumes에서 해당 캐시 위치를 윈도 머신과 다시 연결해주자. 

```yml
        volumes: 
            - /mnt/c/Users/anari/github:/home/rstudio/github-anari
            - /mnt/c/Users/anari/renv:/home/rstudio/renv
        ports: 
            - 8787:8787
        environment: 
            #- DISABLE_AUTH=true
            - PASSWORD=1022
            - ROOT=TRUE 
            - RENV_PATHS_CACHE=/home/rstudio/renv
```

- 일정 환경(프로젝트 로딩)에서 renv 설치 후 아래 명령을 실행해준다. 

```r
Sys.setenv(R_INSTALL_STAGED = FALSE)
```

테스트 삼아 xml2를 설치해보자. `install.packages('xml2')`
