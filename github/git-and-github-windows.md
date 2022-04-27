# git-and-github-in-windows

## Why 
- 터미널에서 원도에서 깃과 깃허브의 관계를 설정하기가 쉽지 않다. 


## Solution 

### Bottomline 
- powershell에서 윈도우용 git을 설치한다. 
	- 윈도 터미널을 완전히 껐다가 다시 켠다. 
- 깃허브 CLI를 설치한다. 
	- `gh auth login`을 통해서 로그인을 해준다. 

### Plain use 
- 그냥 쓸 때는 github desktop을 쓰면 되겠다. 

### In Powershell

- git 설치 
	- 설치 후에는 윈도 터미널을 완전히 빠져나간 후 다시 실행. 그래야 git이 인식된다. 
```powershell
winget install -e --id Git.Git
```

- github CLI 설치 
	- 설치 후에 `gh` 명령어를 통해서 github에 로그인 한다. 
```powershell
winget install -e --id GitHub.cli
gh auth login 
```


### WSL 
- WSL은 별도의 OS 이기 때문에 WSL 상에서 github에 접근하려면 상당한 애로 사항이 있다. 
- gh CLI를 설치한다고 해도 인증이 되지는 않는다. 
	- 윈도용 자격 증명을 가져오라는 것이 해법 

https://docs.microsoft.com/ko-kr/windows/wsl/tutorials/wsl-git

```bash 
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/libexec/git-core/git-credential-manager-core.exe"
```
