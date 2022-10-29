# 우분투 git 버전 업데이트  

Ubuntu에서 git 버전이 최신 버전이 아닐 때 업데이트하는 방법 

## Why 

- `git init -b` 등의 최신 명령어를 쓸 수 없기 때문이다! 

## How 

```shell
$ sudo add-apt-repository ppa:git-core/ppa -y 
$ sudo apt-get update 
$ sudo apt-get install git -y
```

- 마치고 난 후 `git version`으로 확인해보자. 
