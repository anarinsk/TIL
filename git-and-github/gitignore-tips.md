# gitignore tips

| :memo:        | `.gitignore` 관련 팁을 모아보자.      |
|---------------|:------------------------|

## 이미 add된 파일을 무시하고 싶을 때 

[directory - How to git ignore subfolders / subdirectories? - Stack Overflow](https://stackoverflow.com/questions/2545602/how-to-git-ignore-subfolders-subdirectories)

```bash
$ git rm -r --cached .
```

