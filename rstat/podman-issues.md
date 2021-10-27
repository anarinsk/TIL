# Podman Issues 

## project + renv in podman 

https://github.com/anarinsk/setup-docker_compose 
- `.yml` 및 dockerfile 참고 

### What 

- rootless 컨테이너(podman)으로 rocker 이미지를 올렸을 때 project + renv가 제대로 작동하지 않는다. 

### Why 

- renv를 쓰지 않으면 되지만, 왠지 궁금하다. 

### How: Sapjil 

- 우선 `.yml` 파일을 집중적으로 살펴봤지만 크게 도움을 얻지 못했다. 
    + 컨테이너 내에서 연결된 볼륨의 내용을 수정할 수 있는지 여부와 이 이슈는 별개의 이슈다. 
    + WSL에서는 권한 문제가 없고 Ubuntu에서는 폴더를 고칠 수 있는지 없는지에 관한 권한 이슈가 있다. 이건 따로 정리하도록 하자. 
- dockerfile의 수정 역시 초기에는 큰 도움을 주지 못했다. 

### How: Solution 

#### dockerfile 

- home에 `.Rprofile`을 심는다. 
- dockerfile에서 처리가 가능하다. 

```shell
RUN R -e "install.packages(c('renv', 'devtools'))" \
    && echo "Sys.setenv(R_INSTALL_STAGED = FALSE)" >> /home/rstudio/.Rprofile \
```

- 첫번째 명령어는 패키지를 설치하는 명령어다. 반드시 필요한 것은 아니다. 
- 두번째 명령어가 중요. 이 옵셥을 `.Rprofile`에 심도록 하자. 

#### RStudio 

- 프로젝트를 올린다. 
- 메뉴에서 프로젝트 옵션으로 간다. 
    + 옵션 탭에서 renv를 기본으로 활성화하는 옵션을 택한다. 
- 아마 에러가 뜰 것이다. 
    + 상단 메뉴 둘째 줄에서 해당 프로젝트를 클릭해서 프로젝트를 다시 로드한다. 
- 이제 renv를 활성화해보자. 큰 이슈가 없을 것이다. 

## Permission in Ubuntu 

### What 

- Ubuntu에서 구동되는 rocker 컨테이너 이미지에서 연결된 디렉토리를 조작할 수 없는 문제 
    + 디렉토리의 생성, 디렉토리/파일 삭제 등 불가 

### How: solution 

- 도커 생성시 권한을 조정해주자. 

```shell
&& usermod -G root rstudio \
&& umask 000
```

- rstudio 이용자를 root에 편입 
- 새로 생성되는 디렉토리 및 파일의 권한을 최소한으로 설정 