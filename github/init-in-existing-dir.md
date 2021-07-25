# 기존의 활용 폴더를 git 폴더로 만들고 github과 연결하기 

## Where

- https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line

## What 

- gh 명령어를 활용한다. 
- 문제가 되는 지점을 확인한다. 

## How 

- `gh repo create 계정명/리포명`과 같이 깃헙에 리포를 생성한다. 
- 몇 가지 문답이 오고간다. 마지막에 이미 있는 디렉토리를 활용하는 것이기 때문에 디렉토리 생성은 n를 선택한다. 

나머지 프로세스는 통상적인 git initialization을 그대로 따른다. 

```shell
$ git init -b main
$ git add .
# Adds the files in the local repository and stages them for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.

$ git commit -m "First commit"
# Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.

$ git remote add origin  <REMOTE_URL> 
# Sets the new remote
$ git remote -v
# Verifies the new remote URL

$ git push origin main
# Pushes the changes in your local repository up to the remote repository you specified as the origin
```
- `git init -b main` 명령을 쓰려면 git version이 2.32.0 이상이어야 한다. 필요한 경우 git을 업그레이드해줘야 한다. [여기](https://github.com/anarinsk/til/blob/master/github/how-to-update-git-ubuntu.md) 참고. 
- 리포 생성과정에서 `.gitignore`와 같이 로컬에 없는 파일을 생성했다면 push가 되지 않을 수 있다. 
- 이런 경우에는 pull을 한번 하고 푸시를 한다. 
- 이때 pull도 원활하지 않을 수 있는데, 이 경우 해당 메시지를 git이 보여주니 이걸 보고 대처하면 되겠다. 

```text
hint: Pulling without specifying how to reconcile divergent branches is
hint: discouraged. You can squelch this message by running one of the following
hint: commands sometime before your next pull:
hint:
hint:   git config pull.rebase false  # merge (the default strategy)
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
hint:
hint: You can replace "git config" with "git config --global" to set a default
hint: preference for all repositories. You can also pass --rebase, --no-rebase,
hint: or --ff-only on the command line to override the configured default per
hint: invocation.
```

- 갈라진 브랜치를 어떻게 처리할 것인지의 디폴트 액션에 관한 것이다. `git config pull.rebase true` 선택하면 큰 문제는 없을 것이다. 
