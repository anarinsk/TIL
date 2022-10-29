# 파워셸에서 bash 쓰기 

https://github.com/mikebattista/PowerShell-WSL-Interop

## Prerequisites

- WSL 설치 

## Sequence 

1. install `sudo apt install bash-completion` in WSL 
2. install `Install-Module WslInterop` in Powershell 
3. set command in Powershell; 

```
Import-WslCommand "apt", "awk", "emacs", "grep", "head", "less", "ls", "man", "sed", "seq", "ssh", "sudo", "tail", "vim" 
```