# WSL에 conda 없이 Python 설치 

## Bootup!
- 우분투에 설치하는 것과 동일하다. 
- macos의 방법과 크게 다르지 않다. 

## Version 3.10 

SRC: [Ubuntu 3.10에 Python 20.04을 설치하는 방법 - LinuxCapable](https://www.linuxcapable.com/ko/how-to-install-python-3-10-on-ubuntu-20-04/)

- 3.10 버전 설치를 위해서는 리포를 추가해야 한다. 
```bash
$ sudo apt install software-properties-common -y
$ sudo add-apt-repository ppa:deadsnakes/ppa -y
$ sudo apt install python3.10

```

- 기타 필요한 것들도 깔아주자 
```bash
$ sudo apt install python3.10-dev
$ sudo apt install python3.10-venv
$ sudo apt install python3.10-distutils
```

## Symlink 
- 처음 `python -V`를 쳐보면 어떤 python이 디폴트로 잡혀 있는지 알게 된다. 
	- 이 녀석은 `\usr\bin`에 물려 있는 녀석이다. 여기 물린 녀석이 모든 디렉토리에서 실행된다. 실행의 우선권이 부여된다. 

```txt
lrwxrwxrwx 1 root root 19 Jul 11 08:15 python -> /usr/bin/python3.10  
lrwxrwxrwx 1 root root 9 Mar 13 2020 python3 -> python3.8  
-rwxr-xr-x 1 root root 5793336 Jun 12 01:53 python3.10
```
- 위에서 보듯이 심링크로 물여 있다. 각각 아래와 같다. 
	- `python` -> python3.10 
	- `python3` -> python3.8 
	- python3.10 

- 이 지시 관계를 바꿔줄 수 있는 것이 symlink이다. 아래는 3.10 버전을 기본으로 걸어준 것이다. 아래 명령을 실행한 후 `python -V`로 확인해보면 된다. 

```bash
$  ln -s /usr/bin/python3.10 /usr/bin/python
```


## Venv 
- 파이썬 내장 가상환경이므로 이 녀석을 쓰는 게 좋겠다. `pyenv`보다 나을 듯. 

### 생성 
- `~/.venv`를 가상 환경의 기본 디렉토리로 두자. 해당 디렉토리로 이동하자. 

```bash
$ python -m venv test-pytorch
```
- 현재 디렉토리 아래 `test-pytorch`라는 디렉토리가 생성된다. 
- 이 디렉토리 아래 `/bin` 디렉토리가 있다. 
- 이 위치에서 `$ source activate`를 하면 해당 가상 환경이 활성화된다. 
- 필요한 패키지가 있다면 가상 환경 활성화 이후 설치하자. 
- pip 업그레이드가 최우선이다. 
```bash
$ python -m pip install --upgrade pip 
$ python -m pip install pytorch 
```

#### `/bin` 조금 더 보기 
- 이 폴더에 보면 가상 환경이 어떤 파이썬 실행파일을 물고 있는지 보인다. 
- symlink들을 유심히 보자. 

```txt
lrwxrwxrwx 1 anari anari 15 Jul 12 08:52 python -> /usr/bin/python  
lrwxrwxrwx 1 anari anari 6 Jul 12 08:52 python3 -> python  
lrwxrwxrwx 1 anari anari 6 Jul 12 08:52 python3.10 -> python
```

## VS Code 

- Macos VS Code 항목 참고 

## Font 추가 

- macos와 달리 이 대목이 어렵다. macos는 unix 기반이라서 시스템폰트가 잘 인식된다. 하지만 wsl은 별도의 시스템이기 때문에 현재로서는 폰트를 공유하지 않는다. 
- 가끔 matplotlib의 상태가 별로일 때가 있다. 
	- 폰트 리스트가 어떻게 해도 업데이트되지 않는다든가... 
	- 
```bash
python -m pip install --upgrade --force-reinstall matplotlib
```

### Windows 폰트 공유
- 윈도 폰트가 인식이 되기는 하나 D2Coding은 되지 않는다... 
[WSL에서 Windows font 사용하기 (pinedance.github.io)](http://pinedance.github.io/blog/2021/02/08/WSL-fonts)

### D2Coding 폰트 설치 
- nerd 폰트로 설치하자. 
- - [kelvinks/D2Coding_Nerd: D2Coding 1.3.2 Version Nerd Patch (github.com)](https://github.com/kelvinks/D2Coding_Nerd)
	- 다운받을 떄 주의해야 한다. Download의 링크를 따서 주소를 붙여 넣자

```bash
$ mkdir ~/.local/share/fonts
$ cd ~/.local/share/fonts
$ wget [아래 주]
```

- 폰트 재설정 

```bash
# WSL 폰트 재설정 
fc-cache -f -v 
```

- 간혹 matplotlib의 캐시를 지워줘야 할 때가 있다. 캐시 주소 확인해서 지워주자. 