## Macos 

- brew를 통해 인스톨 한다. 
	- python3, pip3 임을 유념하자.
	- alias 지정으로 python3 -> python  
	- 아니면 symlink를 활용하자. 

### python 3.10 설치 
- [python@3.10 — Homebrew Formulae](https://formulae.brew.sh/formula/python@3.10)
- 설치 위치: `/opt/homebrew/opt/python@3.10/bin`

### python 기본 버전 교체 
- 기본 버전은 그대로 두고 쓰자. 어차피 가상 환경이 필요하지 않은가? 

### 가상환경 만들기 
```
> /opt/homebrew/opt/python@3.10/bin/python3 -m venv ~/venv/3.10/pandas
```

## VS Code 
- 일단 커널을 설정을 해야 한다. 그냥 가상 환경만 잡으면 자동으로 인식되지는 않는다. 
- F1 > "Python: 인터프리터 선택"
	- {해당 가상 환경의 디렉토리}/bin/python 까지 지정해준다. 

### kernel 관리 
- 주피터 커널과 vs code  자체에서 관리하는 커널이 있다. 
- 주피터 커널 삭제하는 방법은 아래 같다. 
[python - VSCode Jupyter cannot update kernels automatically - Stack Overflow](https://stackoverflow.com/questions/65858621/vscode-jupyter-cannot-update-kernels-automatically)
- VS 코드 커널 관리는 
	- F1 >  "Python: 인터프리터 선택" 선택하면 오른쪽 위에 리프레시 아이콘이 있다. 이 녀석 누르면 잘 업데이트 된다. 

