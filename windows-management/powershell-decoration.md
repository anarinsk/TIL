# Powershell의 데코레이션 요소를 모아보자. 

## 폰트 바꾸기 

1. Install D2 Nerd Font [kelvinks/D2Coding_Nerd: D2Coding 1.3.2 Version Nerd Patch (github.com)](https://github.com/kelvinks/D2Coding_Nerd)
2. WT의 각 앱별 설정 -> "모양" 에서 바꾸자.  

## Oh My Posh 설치 

[Windows 터미널 사용자 지정 프롬프트 설정 | Microsoft Docs](https://docs.microsoft.com/ko-kr/windows/terminal/tutorials/custom-prompt-setup)

[Oh My Posh - winstall](https://winstall.app/apps/JanDeDobbeleer.OhMyPosh)
- 위 안내 페이지 따라서 설정한다. 
- Nerd 폰트도 설치할 수 있다. 

### 간단 요약 

- 테마 설치 https://ohmyposh.dev/docs/themes
- 테마 적용 https://learn.microsoft.com/ko-kr/windows/terminal/tutorials/custom-prompt-setup#choose-and-apply-a-powershell-prompt-theme
	- `"$env:POSH_THEMES_PATH\paradox.omp.json"` | 이 부분에서 테마 이름은 {파일-이름}.omp.json 
	- "agnosterplus"를 권한다. 
		- agnoster를 쓰니 conda env가 나오지 않더라... 
	- conda env가 나오게 하려면 아래 부분이 있는지 체크해보자. 
```
	{
  "foreground": "#FFE873",
  "leading_diamond": "\ue0b6",
  "style": "diamond",
  "properties": {
    "fetch_virtual_env": true,
    "display_mode": "environment",
    "home_enabled": true
  },
  "template": "\ue235 {{ if .Error }}{{ .Error }}{{ else }}{{ if .Venv }}{{ .Venv }} {{ end }}{{ .Full }}{{ end }}",
  "trailing_diamond": "\ue0b4 ",
  "type": "python"
}
```

### 주의 사항 
- Python(conda) 가상 환경은 `~`에서는 표시되지 않는다!
- 특정 디렉토리를 옮기면 거기서 표현된다. 
- git도 마찬가지 

