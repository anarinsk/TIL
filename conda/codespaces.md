# 총평 
- 베타권 받아서 해봤다. 
- 의외로 아주 편하다. 


# Activate 
- 깃헙 리포를 먼저 만들고
- 이 녀석을 코드 스페이스로 연결해주면 기본 세팅은 끝 

## VS Code extension 

- VS Code 원격 접속 항목에 "코드공간에 연결"이 생긴다. 

# python_tutorials 

## Installation 
- 미니 콘다부터 설치. 터미날에서 설치한다. 

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

```

- 맘바도 설치하자. 

> [!INFO] 
> 터미널 리부트 하는 법 `> exit`를 치고 터미널을 다시 호출하자. 
```bash
$ conda install mamba -n base -c conda-forge
```

- 이제 환경을 세팅하자. 

```bash
$ mamba create -n python10+pandas python=3.10
$ mamba env list
$ mamba init # 최초 1회 필요 
$ mamba activate python10+pandas

```

## Jupyter 
- 안에서 주피터 파일(`.ipynb`)을 띄우면 커맨드 창에 알아서 설치 명령어가 뜬다. 그대로 terminal에 복붙에서 실행하면 된다. 

# Problems to be solved 

## 작업 환경 보존 

- 그냥 잘 되는 것 같다... 

## 한글 폰트 설치 

### 터미널 내에서 font download 

- 폰트를 저장할 주소로 이동 

```
? cd /usr/share/fonts/truetype/
? sudo mkdir d2coding 
? cd d2coding 
```

- 폰트를 다운로드 한다. 
	- 깃헙에서 다운로드할 때 주의. 그냥 `.com` 주소를 붙이면 인식이 되지 않는다. 
		[Revisions to Download single files from GitHub - Stack Overflow](https://stackoverflow.com/posts/4605068/revisions)

````
https://raw.githubusercontent.com/user/repository/branch/filename
````

이 주소 체계로 써줘야 한다.  for example 

```
? sudo wget https://raw.githubusercontent.com/kelvinks/D2Coding_Nerd/master/D2Coding%20v.1.3.2%20Nerd%20Font%20Complete.ttf`
```

### 해당 폰트 인식 

```
? sudo fc-cache -f -v 
```

- `f`: 강제로 스캔하라는 뜻, `v`: verbose 결과를 자세히 상술하라는 뜻 
- 잘 되었나 확인은 `fc-list`

### Jupyter 설정 


```python
import platform
print(f"Platform is {platform.platform()}")
import sys
print(f"Version of python is {sys.version_info}")
import matplotlib
import matplotlib as mpl

  

print ('matplotlib 정보-------------')
print ('버전: ', matplotlib.__version__)
print ('설치위치: ', matplotlib.__file__)
print ('설정: ', matplotlib.get_configdir())
print ('캐시: ', matplotlib.get_cachedir())

mpl.rcParams['font.family'] = 'D2Coding Nerd Font'
mpl.rcParams['axes.unicode_minus']  = False
```

- 마지막 두 줄이 주피터용 폰트 설정이다.  D2Coding Nerd Font가 잘 설치되었는지는 아래와 같은 명령으로 주피터에서 확인해볼 수 있다. 

```python
import matplotlib.font_manager
[f.name for f in matplotlib.font_manager.fontManager.ttflist if 'D2' in f.name]
```

### 체크용 코드 

```python
import numpy as np
  

data = np.random.randint(-100, 100, 50).cumsum()

import matplotlib.pyplot as plt
plt.plot(range(50), data, 'r')
plt.title('가격변동 추이')
plt.ylabel('가격')
plt.show()
```

## Container 구동 
