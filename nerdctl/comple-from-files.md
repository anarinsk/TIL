파일에서 컴파일하는 방법 

## View 

- 컨테이너 조회 
```
nerdctl ps 
```

- 이미지 조회 
```
nerdctl images 
```

- 이미지 삭제 
```
nerdctl rmi $(nerdctl images -qa)
```
- `-a`: all
- `-q`: quiet 모드(id만 표시)


## Build 

```
nerdctl build -f FILE-NAME .
```

- 아주 기본적인 빌드 
- 빌드된 이미지는 `nerdctl images`로 확인하자. 

```
nerdctl build -f Dockerfile.nerd -t anarinsk/jupyter-ds-korfont:m1 .
```
- `-f`: file name 
- `-t`: name and tag by "NAME:TAG"

## Run 

```
nerdctl run -it --rm -v $PWD:/home/jovyan/work -u root -e JUPYTER_TOKEN=1022 -e GRANT_SUDO=yes -p 10000:8888 anarinsk/jupyter-ds-korfont:m1
```
- `-i`: interactive
- `-t`: Allocate a pseudo-TTY
- `--rm`: remove when exiting 
- `-v`: volume 
- `-u`: user 
- `-e`: env 
- `-p`: port forwarding 

### `-u` 옵션의 의미 
- k8s에서 컨테이너를 올릴 때에는 -u 옵션이 없다. 
- 빌드 단계에서 `USER root`를 설정해주면 된다. 
	- 만일 안해주면 bash에서 `sudo` 먹지 않는다. 

## Push 

- dockerhub 로그인 
```
nerdctl login 
```

```
nerdctl push anarinsk/jupyter-ds-korfont:m1
```