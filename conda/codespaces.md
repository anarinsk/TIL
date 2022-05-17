# 총평 
- 베타권 받아서 해봤다. 
- 의외로 아주 편하다. 


# Activate 
- 깃헙 리포를 먼저 만들고
- 이 녀석을 코드 스페이스로 연결해주면 기본 세팅은 끝 

## VS Code extension 

- VS Code 원격 접속 항목에 "코드공간에 연결"이 생긴다. 

# python_tutorials 

## Installation 
- 미니 콘다부터 설치. 터미날에서 설치한다. 

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

```

- 맘바도 설치하자. 

> [!INFO] 
> 터미널 리부트 하는 법 `> exit`를 치고 터미널을 다시 호출하자. 
```bash
$ conda install mamba -n base -c conda-forge
```

- 이제 환경을 세팅하자. 

```bash
$ mamba create -n python10+pandas python=3.10
$ mamba env list
$ mamba init # 최초 1회 필요 
$ mamba activate python10+pandas

```

## Jupyter 
- 안에서 주피터 파일(`.ipynb`)을 띄우면 커맨드 창에 알아서 설치 명령어가 뜬다. 그대로 terminal에 복붙에서 실행하면 된다. 

# Problems to be solved 

## 작업 환경 보존 

## 한글 폰트 설치 
