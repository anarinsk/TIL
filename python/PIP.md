## Macos 

- brew를 통해 인스톨 한다. 
	- python3, pip3 임을 유념하자.
	- alias 지정으로 python3 -> python  

### python 3.10 설치 
- [python@3.10 — Homebrew Formulae](https://formulae.brew.sh/formula/python@3.10)
- 설치 위치: `/opt/homebrew/opt/python@3.10/bin`

### python 기본 버전 교체 
- 기본 버전은 그대로 두고 쓰자. 어차피 가상 환경이 필요하지 않은가? 

### 가상환경 만들기 
```
> /opt/homebrew/opt/python@3.10/bin/python3 -m venv ~/venv/3.10/pandas
```

### VS Code 
- F1 > Python: 인터프리터 검색 
- 여기에서 가상 환경 주소를 넣어주자. 
```
{venv}/bin/python 
```
