# Winget으로 설치하자. 

- Winget을 활성화하기 위해서는 windows store에서 "앱 설치 관리자"를 찾아서 활성화 

https://docs.microsoft.com/ko-kr/windows/package-manager/winget/

- 아래와 같은 방식으로 활용할 수 있다. 

```Shell
winget install powershell 
winget install vscode 
winget install -e --id Docker.DockerDesktop
winget install -e --id Microsoft.WindowsTerminal
```

https://winstall.app/

광범위한 윈겟 활용방법. 버전 별 설치 등등이 나열되어 있다. 

## Upgrade with winget 

```shell
1> winget upgrade 
2> winget upgrade --all 
```

1. 업그레이드 가능한 항목을 보여준다. 
2. `--all` flag로 모든 항목을 업데이트한다. 
- Windows Terminal 자체도 업그레이드 대상이므로 기본 터미널 같은 것을 이용하도록 하자. 

##  Microsoft Store가 없는 경우 

- 이거 상당히 골치아픈 경우다. 
- 우선, `설정` > `업데이트 및 보안` > `개발자용`, 개발자 모드를 활성화해주자. 

### 프레임워크를 먼저 설치하자. 

- Powershell 관리자모드로 실행해야 한다. 
  + 그런데 관리자 모드를 실행하면 파일 경로 붙이기 기능이 돌지 않는다. 그러므로 둘 다 띄워둔다. 

- 데스크톱 브릿지 appx를 먼저 설치해야 한다. https://docs.microsoft.com/ko-kr/troubleshoot/cpp/c-runtime-packages-desktop-bridge
  + 64비트 용으로 OS에 맞게 잘 받자. 
  + 관리자 모드가 아닌 파워셸에서 아래와 같이 `App-AppxPackge` 타이핑한 후 다운로드한 파일을 드래그앤드룹하면 경로가 붙는다. 
  + 이 녀석을 다시 복사해서 관리자 모드의 파워셸에 붙여 넣고 실행한다. 

```shell
Add-AppxPackage <file.appx> 
```

### Winget을 설치하자. 

- 같은 방식으로 winget을 설치할 수 있다. 파일 경우른 다음과 같다. 
- https://github.com/microsoft/winget-cli/releases
- 여기서 `appxbundle` 확장자 파일을 다운로드 받는다. 
