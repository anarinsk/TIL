## 기본 정보 
- 공식 사이트의 도큐멘테이션이 그다지 친절하지는 않다. 

## Basic Setups 

```python
import panel as pn
pn.extension()
```

- 만일 Jupyter에서 interactive한 동작을 원한다면, 

```
pn.extension(comms='ipywidgets')
```

- 추가로 설치해야 하는 패키지가 있을 수 있으니 주의 요망 

## Pyscript 
- 파이 스크립트와 함께 쓸 떄 강력할 것이다. 
- VS Code에서 "Live Preview"를 설치하자. 
	- html에서 프리뷰 버튼을 볼 수 있다. 오른쪽 창에 띄우고 실시간 코드 수정이 가능하다. 

```
<html>
    <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-2.4.2.js"></script>
    <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-widgets-2.4.2.min.js"></script>
    <script type="text/javascript" src="https://cdn.bokeh.org/bokeh/release/bokeh-tables-2.4.2.min.js"></script>
    <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/@holoviz/panel@0.13.1/dist/panel.min.js"></script>
 
    <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css" />
    <script defer src="https://pyscript.net/alpha/pyscript.js"></script>

    <title>
    Summarized View of IP Based on CMS
    </title>

    <!---pyodide-->

    <py-env>
        - pandas
        - openpyxl
        - panel == 0.13.1
        - matplotlib
        - numpy
        - koreanize_matplotlib
        - paths:
            - ./sample.xlsx
            - ./main_panel_test.py

    </py-env>
    </head>

    <body>
        <py-script src="main_panel_test.py">    
        </py-script>

    </body>

</html>
```

- html의 기본 구조를 간단히 살펴보자. 
	- `<title>` 태그 시작 전까지는 panel 및 pyscript 로드하는 부분이다. 
	- `<py-env>`는 다음과 같다. 
		- 필요한 패키지 로드 
		- 로컬 디렉토리 패스에서 활용할 파일 설정 
- 원래 `<py-script>` 태그 사이에 python 명령을 넣는다. 위의 예제처럼 `.py`을 독립해 넣는 것이 깔끔하다. 

