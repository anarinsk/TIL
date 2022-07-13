# Install
[Quarto - Get Started](https://quarto.org/docs/get-started/)

## Basic command 

```bash
$ quarto --version 
$ quarto render 
$ quarto preview 
```

## Ubuntu 

```
dpkg -i package_file.deb
```

## Macos 
- 그냥 설치하면 된다. 
- 앱을  깔 때 모든 이용자 설치하면 되지 않았다. 이 점 유의!
	- 윈도, 맥 공히 해당한다. 
	- 설치 위치 변경 옵션을 누르면 개별 사용자 설치 화면이 뜬다. 
		- `/Users/anari/Applications/quarto/`

## Code implementing 
- 코드 실행은 qmd의 커다란 장점이다.  
- 그런데 이 장점을 다 누리려면 가상 환경 상황에서 qmd를 컴파일할 수 있어야 한다. 
- VS Code Extension에서 어떤 가상환경이 적용되는가? 
	- conda : 안된다. 
	- venv: 가능하다! 단 `nbformat`, `nbclient`만 환경에 설치하면 된다. 

## Problems 

#### Installation 
- 모든 이용자 설치시 `Applications/quarto/bin`에 설치된다. 
	- 해당 패스가 `.zshrc`에 잡혀 있지 않은 관계로 발생하는 문제? 
	- 1.0.X 버전에서는 해결된 것으로 추측... 


### 옵션 에러 
- 버전 1.0.4 
- index.qmd의 `feed:true` 상태에서 컴파일 시 윈도, 리눅스 모두 에러가 뜬다. 