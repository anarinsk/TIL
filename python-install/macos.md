# Macos without conda 

- brew를 통해 인스톨 한다. 
	- 관리상의 이유 
	- python3, pip3 임을 유념하자.
	- 디폴트 혹은 대표 `python` 지정
		- alias 지정으로 python3 -> python ?
		- symlink?

## python 3.10 설치 
- [python@3.10 — Homebrew Formulae](https://formulae.brew.sh/formula/python@3.10)
- 설치 위치: `/opt/homebrew/opt/python@3.10/bin`

## python 기본 버전 교체 
- 기본 버전은 그대로 두고 쓰자. 어차피 가상 환경이 필요하지 않은가? 

## 가상환경 만들기 
- 특정 위치의 파이썬을 실행하려면 
```bash
$ /opt/homebrew/opt/python@3.10/bin/python3 -m venv ~/venv/3.10/pandas
```
- 대표 파이썬이 지정되어 있다면, `python`만 쓰면 된다. 

## VS Code 

### Bootup!
- 인터프리터와 커널의 차이점을 이해하자. 
	- 인터프리터: VS Code 전반이 이해하는 파이썬 및 언어의 환경 / terminal 환경과 관련 
	- 커널: Jupyter Extension의 실행 환경, 	커널을 바꿨다고 해서 인터프리터가 주관하는 터미널 창의 환경이 바뀌지는 않는다! 

### 인터프리터선택
- F1 > "Python: 인터프리터 선택"
	- `{해당 가상 환경의 디렉토리}/bin/python` 까지 지정해준다. 
	- 위에 리프레시 버튼을 누르면 으너 정도는 자동으로 조정된다. 
	- 여기 선택된 가상 환경에 따라서 터미널 창이 연동된다. 

### kernel 관리 
- 주피터 커널 삭제하는 방법은 아래 같다. 
[python - VSCode Jupyter cannot update kernels automatically - Stack Overflow](https://stackoverflow.com/questions/65858621/vscode-jupyter-cannot-update-kernels-automatically)

## 폰트 추가 
- wsl 참고 


