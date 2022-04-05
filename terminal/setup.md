# Setup terminal 

## Fonts 

- 한글 폰트는 아래 두 개를 깔자 
    + https://github.com/kelvinks/D2Coding_Nerd   

## WSL, Ubunutu, macos 

### zsh 

- zsh을 OS에 맞춰서 설치하자. https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH
- 기본 셸로 설정하자. 
    + wsl에서는 설치하고 oh-my-zsh 설치하면 zsh를 디폴트 셸로 쓸 건지 물어본다. 
    
### oh-my-zsh 

- https://ohmyz.sh/

### powerlevel 10k 

- https://github.com/romkatv/powerlevel10k#installation
-   + 주의할 것은 `.zshrc`에서 `ZSH_THEME` 수정할 떄 기존 것을 수정해줘야 한다. 
- 깔고나서 다시 실행하면 자동으로 인스톨 스테이지로 들어간다. 
    + 만일 아니라면, `power10k configure`

## Powershell 

파워셸 꾸미기 
https://docs.microsoft.com/en-us/windows/terminal/tutorials/custom-prompt-setup

파워셸에서 bash 명령어 쓰기 
https://github.com/mikebattista/PowerShell-WSL-Interop

- powershell profile의 위치는 terminal에서 
```
$PROFILE | Get-Member -Type NoteProperty
```
