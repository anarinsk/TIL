# 그림 크기 조절 및 배열 정렬하는 다양한 방법 

## 일반 문서 내 정렬 

[Quarto - Figures](https://quarto.org/docs/authoring/figures.html)

- `:::`을 활용하면 된다. 
- 만일 하나의 그림의 크기를 조절하고 싶다면 
```
::: {layout="[[70,30], [100]]"}
```
> [!Code Tip]
> - 위의 사례를 3개의 그림을 위에 두 개, 아래 하나를 배치한다. 
> - 각각의 숫자는 그림의 비율을 나타낸다. 
> - 만일 중간에 공백을 삽입하고 싶다면, `[70,30]` -> `[50,-10,20]`

## 코드 내 정렬 

- 원리는 동일하다. 

```{python}
#| layout: "[-10,70,-10]"

import matplotlib as mpl
import matplotlib.pyplot as plt
import matplotlib.font_manager as fm
import numpy as np

# 그릴 데이터 생성
def draw_sample(fontprop=None):
	data = np.random.randint(-100, 100, 50).cumsum()
	plt.plot(range(50), data, 'r')
	plt.title('가격변동 추이', fontproperties=fontprop)
	plt.ylabel('가격', fontproperties=fontprop)
	plt.show()

draw_sample()
```

> [!Code Tip]
> - `#|` 해당 코드 내에 생성되는 그림의 양식을 지정한다. 
> - 여기서는 생성되는 그림이 하나이므로, 양쪽의 -10은 좌우의 여백에 해당한다. 

