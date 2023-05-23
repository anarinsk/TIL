# WSL 설치 관련된 기본 사항을 정리해둔다. 

## Why 

- Legacy 문서를 TIL 안으로 정리해둔다. 

## Daily Use & Management

https://github.com/anarinsk/setup-wsl-daily_use

## General Guide 

https://www.guide2wsl.com

## nerdctl 

https://www.guide2wsl.com/nerdctl/#setuid-bit-tells-nerdctl-which-user-to-use

### 설치시 주의사항 

- 내부의 명령어를 풀어서 이해하면 된다. 

```shell=
wget -q "https://github.com/containerd/nerdctl/releases/download/v${NERDCTL_VERSION}/nerdctl-full-${NERDCTL_VERSION}-linux-${archType}.tar.gz" -O /tmp/nerdctl.tar.gz
```

- 파일 링크를 `" "` 안에 직접 써주면 된다. 

```shell=
echo -e '\nexport PATH="${PATH}:~/.local/bin"' >> ~/.bashrc
```

`~/.local/bin` 대신 `/home/{유저이름}/.local/bin`으로 명시하자. 




