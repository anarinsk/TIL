# Miniforge for win11

## Why 
- 윈도우즈 11에서 미니포지3 관리하기 

## 설치 
- 미니포지3 윈도우즈 설치 파일 다운로드 [conda-forge/miniforge: A conda-forge distribution. (github.com)](https://github.com/conda-forge/miniforge)
	- 모든 사용자 용으로 설치한다. 
- winget으로 다 까는 게 목표다. 
	- 가상 환경 인식 문제 등등을 살펴보자. 
	- 설치경로는 `C:\Users\{USER NAME}\miniforge3`
	- 스크립터 경로는 `C:\Users\{USER NAME}\miniforge3\Script`
	- VS Code에서 인터프리터 선택 인식에서 문제 없었다. 
- ~~winget으로 설치하면 안되는 이유
	- winget은 `C:\Users\{이용자ID}\appdata\miniforge3` 으로 설치되며, 가상 환경 등도 마찬가지로 설치  
- 이렇게 설치하면 가상 환경 등이 `C:\Users\{이용자ID}\.conda\envs\`로 설치 된다. 
	- 이 경우 VS Code 등에서 python 인터프리터가 인식된다.

## 설정 
- ~~miniforge 프롬프트가 같이 설치된다. 애를 먼저 띄운다.~~
	- ~~창에 'conda init powershell'을 실행한다. ~~
	- ~~이러면 WT에서 파워셸로 그냥 쓸 수 있는 상태가 된다. ~~
- 소프트웨어가 설치되는 경로는 다음과 같다. 
	- 다운로드 받아서 설치하면 `C:\ProgramData\miniforge3`
	-  winget은 `C:\Users\{이용자ID}\appdata\local\miniforge3` 으로 설치
	- 가상환경은 `{적당한 공통 항목}\minforge3\envs`
- path를 설정하자. 그래야 터미널, 파워셸에서 `conda` 명령이 인식된다. 
	- Windows + I -> 정보 
	- 장치 사양 아래 "고급 시스템 설정" 
	- "환경 변수"
	- "유저 변수" 아래 Path 클릭 
	- 여기에 `C:\ProgramData\miniforge3\Script`를 추가하도록 하자. 
	- 패스는 한번 잡으면 다시 지우고 설치해도 그대로 유지된다. 

## VS Code 
- 대체로 문제 없이 잘 된다. 
- 콘다 env 환경에서 운용도 가능하다. 
	- F1 -> "Python: 인터프리터 선택" -> 리프레시로 환경 설정

### Quarto Issue 
- 먼저 nbformat, nbclient를 설치하자. 
	- `conda install nbformat nbclient`
- 문제가 되는 것은 Quarto 문서 내에서 코드를 실행하는 경우이다. 
- 필요한 설치를 마친 후에도 렌더링 과정에서 `# [WinError 2] The system cannot find the file specified` 에러가 뜬다. 
- 이떄는 `python -m ipykernel install --user` 로 ipykernel을 유저 레벨로 깔아주면 해결된다. 
- 

