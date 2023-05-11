
파워셸에 관한 모든 설정을 한방에 정리한다. 나머지 md들은 시간이 좀 지나고 지울 예정이다. 

## Install 

### Prelim 
- 원도우즈 터미널(WT)가 세팅되어 있다. 
- MS Store를 통해서 "앱 설치 관리자"가 설치되어 있다. 

```cmd
> winget install --id=Microsoft.PowerShell  -e
```

### Postjob
- 설정에서 기본 프로필 변경: Windows Powershell > Powershell 
- 각 프로필 별로 관리자 권한 실행 
- 모양에서 폰트 설정
	- 설치할 폰트는 Hack Nerd 권장 [Nerd Fonts](https://www.nerdfonts.com/font-downloads)
	- 예비로 D2Coding Nerd도 함께 설치 [D2Coding, Nerd Font 적용 (dante2k.com)](https://www.dante2k.com/602)
	- 글꼴 바꾸기 

## Install Apps 

- winget-install 노트 참고 

## Conda 가상 환경 문제 

Conda를 PS에서 이용하기 위해서는 먼저 초기화가 필요하다. 

```shell
> conda init powershell
```

이 작업을 하고 나서도 가상 환경이 보이지 않을 수 있다. 즉, `conda env list`로 확인 헀을 때 `*`가 보이지 않는 문제다. 우선 이 문제를 확인하기 위해서는 "명령 프롬프트" 창에서 어찌 보이는지 확인해봐야 한다. 만일 명령 프롬프트에서 잘 보인다면, PS 설정에 문제가 있는 것이다. 

### `profile.ps1`이 제대로 로드되지 않는 문제 

원드라이브가 home으로 잡할 때 혹은 home에 한글이 포함되어 있을 때 설정이 담긴 `.ps1` 파일에  PS가 제대로 접근하지 못해서 생기는 문제로 추정된다. 이를 확인해보는 방법은 일단 아래 링크를 참고하자. 

[[Anaconda] Powershell에서 아나콘다 가상환경 활성화가 안 되는 문제 해결하기](https://jh-bk.tistory.com/57)

`conda init powershell`을 실행했을 때 마지막 부분에 ps1를 읽어오는 부분이 포함되어 있다. 이 녀석들이 어찌되어 있는지를 먼저 확인하자. 

```shell
> test-path $profile
```

false가 뜬다면 강제로 다시 설정하자. 

```shell
> new-item -path $profile -itemtype file -force
```

이 상태에서 `conda init powershell`을 다시 실행해준다. 그리고 해당 설정 파일이 생성된 위치를 확인하려면 `$profile`을 타이핑하자. 내 경우 `C:\PowerShell` 아래 설정되었다. 여기에는 여러가지 프로필이 올 수 있다. 파일 이름이 달라도 `.ps1` 확장자를 지닐 경우 PS로드 시 읽어온다.  `conda init powershell`로 설정한 프로필 파일은 `profile.ps1`으로 저장된다. 파일을 읽어보면 conda 관련 설정 스크립트가 들어 있다. 

## Oh-my-posh 설정 

[Home | Oh My Posh](https://ohmyposh.dev/)

winget으로 설치한 이후 필요한 테마를 테스트하면 된다. 

```shell
oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/jandedobbeleer.omp.json" | Invoke-Expression
```

테마가 잘 먹는지 일단 확인해볼 수 있다. 특정 테마를 항상 띄우려면 프로필을 하나 생성해주면 된다. 

```shell
> notepad $profile
```

파일이 없으면 생성된다. 여기에 필요한 테마를 올려주면 된다. 예를 들어, 

```shell
> oh-my-posh init pwsh --config "$env:POSH_THEMES_PATH/powerlevel10k_modern.omp.json" | Invoke-Expression
```

#### 업데이트 시 테마가 초기화되는 문제 

- `$env:POSH_THEMES_PATH`의 위치에 따라서 업데이트 시 테마까지 통으로 업데이트가 된다. 
- 해결책 
	- github https://github.com/anarinsk/setup_posh/ 클론
	- themes에서 필요한 테마 선정 
	- `$profile`을 열어서 테마의 위치 부분을 위의 깃헙 클론 주소로 바꿔준다. 

### Python 가상 환경 이슈 

- 테마에서 conda, python의 가상 환경이 안보일 때가 있다. 
- 테마에서 python 표시되는 분을 찾는다. 이 부분의 적당한 부분에 아래 코드를 넣자. 

```json
"properties": {
    "fetch_virtual_env": true,
    "display_mode": "environment",
    "home_enabled": true
  },
  "template": "\ue235 {{ if .Error }}{{ .Error }}{{ else }}{{ if .Venv }}{{ .Venv }} {{ end }}{{ .Full }}{{ end }}",
  "trailing_diamond": "\ue0b4 ",
  "type": "python"
```


## 일상적인 관리 

```shell
> winget update --all
> conda update --all # 해당 환경에서 실행 
```






