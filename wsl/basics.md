# WSL 설치 관련된 기본 사항을 정리해둔다. 

## Why 

- Legacy 문서를 TIL 안으로 정리해둔다. 

## Daily Use 

https://github.com/anarinsk/setup-wsl-daily_use

## Docker 

- Docker Desktop을 깔면 된다. 
- 유료화되었으므로 되도록 쓰지 않도록 한다. 

### Alternative 1: WSL 2 native 

- systemd를 활성화하고 nerdctl을 깔아서 쓴다. 
- 아직 뭔가 잘 되지 않는다... 
- 참고할 만한 사이트 
  + https://medium.com/geekculture/move-away-from-docker-now-and-utilize-wsl2-systemd-genie-containerd-with-nerdctl-d5f729dcf227
  + https://zenn.dev/dozo/articles/8f52b714d6d430

#### 문제점 (해결될 때까지) 

- medium의 인스트럭션은 해결이 되지 않더라. 
  + systemd를 빠르게 설치하는 스크립트는 제공한다. 
- 일본어 페이지는 설치는 무사히 가능했다. 
  + 다만 이후에 외부 도커 이미지를 끌어오지 못했다. (resolving issue) 

### Alternative 2: Rancher Desktop 

- 도커와 같은 방식을 취한다. 
  + `wsl -l -v`를 쳐보면, rancher-desktop, rancher-desktop-data vm이 존재한다. 

#### 장점 

- preference를 통해서 WSL 인티그레이션을 제공한다. 
  + 활성화가 안될 경우 WSL을 리부팅하면 된다. 
- 그냥 powershell에서 nerdctl등을 사용할 수 있다. 

## Podman 

https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md

## Basic Environment 

- zsh이 좋긴 한데, 매번 설정이 귀찮지 않나? 
- 그냥 bash를 쓰고, starship을 쓰자. 

### why 

- 간단한 설치 
- powershell, wsl, macos 등등에 두루 쓸 수 있다. 

### bash

- https://computingforgeeks.com/how-to-install-starship-shell-prompt-for-bash-zsh-fish/
- curl의 경우 회사에서 문제가 생기니까 소스를 받아서 컴파일하도록 하자. 

```shell
curl -s https://api.github.com/repos/starship/starship/releases/latest \
  | grep browser_download_url \
  | grep x86_64-unknown-linux-gnu \
  | cut -d '"' -f 4 \
  | wget -qi -
#
tar xvf starship-*.tar.gz
#
sudo mv [x86_64-unknown-linux-gnu/]starship /usr/local/bin/
```

- `[...]`는 아마도 필요 없는 부분 

설치 후에 

```shell
# Bash
$ vim ~/.bashrc
eval "$(starship init bash)"
```

### [TMI] Powershell에 깔기 

https://dev.to/ganmahmud/take-your-windows-powershell-to-the-next-level-by-starship-2gb2
