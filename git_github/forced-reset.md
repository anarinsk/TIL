ls 

# 원격 저장소 강제 리셋하는 법 

[version control - Git: How to reset a remote Git repository to remove all commits? - Stack Overflow](https://stackoverflow.com/questions/2006172/git-how-to-reset-a-remote-git-repository-to-remove-all-commits)

- local의 헤당 디렉토리 파일 다 지우기
- 깃 이니셜라이즈 > add > commit 

```shell
$ git init 
$ touch README.md 
$ git add . 
$git commit -m "Reinit"
```

- 원격 저장소를 새로 설정하고, 강제로 푸시한다. 

```
$ git remote add origin <url>
$ git push --force --set-upstream origin main
```

