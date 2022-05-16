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

### Problems 

#### Installation 
- 모든 이용자 설치시 `Applications/quarto/bin`에 설치된다. 
- 해당 패스가 `.zshrc`에 잡혀 있지 않은 관계로 발생하는 문제 
- `nano ~/.zshrc`
	- nano 에디터 창 맨 하단에 `export PATH="/Applications/quarto/bin:$PATH"` 포함 
- 문제는 이렇게 설치하면 vscode에 인식이 되지 않는다. 
- 따라서 개별 사용자 설정으로 설치해야 한다. 설정이 뜨지 않으면 리부트 
- `where quarto`로 위치 검색 
	- `/Users/anari/Applications/quarto/bin/quarto`
- 만일 버전업이 되지 않는다면 수동으로 지우고 재설치  

## Windows 
- 사용자 제한 설치를 하면 문제 없이 잘 업그레이드 된다.  
	- 경로도 보여준다. 

### Problems
- 버전 0.9.393
- index.qmd의 `feed:true`시 컴파일 에러가 뜬다. 