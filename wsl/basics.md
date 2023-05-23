# WSL 설치 관련된 기본 사항을 정리해둔다. 

## Why 

- Legacy 문서를 TIL 안으로 정리해둔다. 

## Daily Use & Management

https://github.com/anarinsk/setup-wsl-daily_use

## General Guide 

https://www.guide2wsl.com

## nerdctl 설치 

https://www.guide2wsl.com/nerdctl/#setuid-bit-tells-nerdctl-which-user-to-use

### Attention

- [배포 버전](https://github.com/containerd/nerdctl/releases)
- sh 스크립트를 만들지 않고 명령어를 풀어서 실행해도 된다. 
- 위 가이드를 응용해서 zsh에 설치하는 명령어는 아래와 같다. 
- 테스트는 링크의 내용을 참고하라. 


```shell=
# Containerd 설치 
> sudo apt install containerd

# nerdctl 다운로드 
# verion 정보와 platform 정보 확인해서 고쳐라. 
# 파일은 /tmp.nerdctl.tar.gz로 저장된다. 
> wget -q "https://github.com/containerd/nerdctl/releases/download/v1.4.0/nerdctl-full-1.4.0-linux-amd64.tar.gz" -O /tmp/nerdctl.tar.gz
> mkdir -p ~/.local/bin
> tar -C ~/.local/bin/ -xzf /tmp/nerdctl.tar.gz --strip-components 1 bin/nerdctl

> echo -e '\nexport PATH="${PATH}:/home/{유저 네임}/.local/bin"' >> ~/.zshrc
> source ~/.zshrc
```

이후 설정은 아래를 참고하라. 

```shell=
# SETUID bit tells nerdctl which user to use
> sudo chown root "$(which nerdctl)"
> sudo chmod +s "$(which nerdctl)"

#Start containerd
> sudo echo -n ; sudo containerd &
sudo chgrp "$(id -gn)" /run/containerd/containerd.sock

#Install the CNI Plugin
> tar -C ~/.local -xzf /tmp/nerdctl.tar.gz libexec
> echo 'export CNI_PATH=/home/{유저 네임}/.local/libexec/cni' >> ~/.zshrc
> source ~/.zshrc
```





