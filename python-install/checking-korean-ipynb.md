```python
import platform
print(f"Platform is {platform.platform()}")
  

import sys
print(f"Version of python is {sys.version_info}")

import matplotlib
print ('matplotlib 정보-------------')
print ('버전: ', matplotlib.__version__)
print ('설치위치: ', matplotlib.__file__)
print ('설정: ', matplotlib.get_configdir())
print ('캐시: ', matplotlib.get_cachedir())
```

- 관련 정보 프리팅

```python
import platf
import matplotlib
import matplotlib.font_manager

#[f.fname for f in matplotlib.font_manager.fontManager.ttflist]
#[f.name for f in matplotlib.font_manager.fontManager.ttflist if 'Nanum' in f.name]
#[f.name for f in matplotlib.font_manager.fontManager.ttflist if 'D2' in f.name]
#[f.name for f in matplotlib.font_manager.fontManager.ttflist if ('D2' in f.name) | ('Nanum' in f.name) ]
#[(f.name, f.fname) for f in matplotlib.font_manager.fontManager.ttflist if ('D2' in f.name) | ('Nanum' in f.name) ]
```

- 폰트 상태 확인 

```python
import platf
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm
import numpy as np

data = np.random.randint(-100, 100, 50).cumsum()

path = '/mnt/c/Windows/Fonts/NanumGothicBold.ttf'
#path = '/usr/share/fonts/truetype/D2CodingLigature/D2Coding-Ver1.3.2-20180524-ligature.ttf'
#path = '/usr/share/fonts/truetype/nanum/NanumBarunGothic.ttf'
fontprop = fm.FontProperties(fname=path, size=18)
```

- 직접 폰트를 지정해 인쇄 
- 윈도 폰트를 불러왔다. 

```python
import platf
import matplotlib.pyplot as plt

plt.rcParams["font.family"] = 'D2Codingligature Nerd Font'
plt.rcParams['font.size'] = 18.
plt.rcParams['xtick.labelsize'] = 12.
plt.rcParams['ytick.labelsize'] = 12.
plt.rcParams['axes.labelsize'] = 14.

plt.rcParams['axes.unicode_minus'] = False
plt.title('가격의 변화')
plt.ylabel('가격')
plt.plot(range(50), data, 'r')
plt.show()
```

- 전역 설정을 바뀌서 인쇄 