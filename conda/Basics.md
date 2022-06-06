1. Installation 
2. Using env
3. Installing jupyer 
4. Installing tensorflow

## Installation 
### m1, linux (WSL)
1. [Miniconda — Conda documentation](https://docs.conda.io/en/latest/miniconda.html)
2. ~/Downloads 디렉으로 이동 
	```
	bash Miniconda3-latest-MacOSX-x86_64.sh
	```

### Windows
- ~~윈도에 꼭 깔아야 하나? 그냥 WSL 2에 깔아서 쓰면 안될까? ~~
	- 윈도에 깔지 말자. 어차피 이득도 없잖아~

### After installation  
- 업데이트 & 업그레이드 
	- 둘 중 하나만 해주면 되는 것 같다... 
	
```
$ conda update conda --all
$ conda upgrade --all
```

### Install mamba 
[mamba-org/mamba: The Fast Cross-Platform Package Manager (github.com)](https://github.com/mamba-org/mamba)

```
conda install mamba -n base -c conda-forge
```

- `conda` 버전과 안 맞아 `mamba`가 부러지는 경우가 있다. 
	- 2022-06-06 현재 conda 4.13.0 mamba가 조응하지 않는다. 

### Uninstall 
- miniconda를 깔았다면 그냥 날려버리면 된다. 

```bash
$ which conda 

```

- 해당 디렉토리를 찾아서 지우자. 

## Using env 
- general ref: [Managing environments — conda 4.12.0.post25+90149568 documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

### create

- 환경이 생성되는 위치는 /Users/username/opt/envs/env-name 아래 
```
mamba create -n MY-ENV python=3.8
```

### check the list of env created
```
mamba env list  
```

### activate / deactivate 
- 액티베이트에는 이름이 필요하지만 디액티베이트에는 필요 없다. 
```
conda activate MY-ENV
conda deactivate 
```

### Best practices 
- 대체로 프로젝트 별로 생성해서 쓰고 버리고 하는 편이 좋겠다. 
- 다만 일상적인 활용을 위해서 pandas 정도를 만들어두고 쓰자. 


### Create yml file for env 
- 일단 환경에 제대로 들어와 있는지부터 확인하자. 
	- `mamba env list`
```
conda env export > MY-ENV.yml
```

### Create env from yml file 
[Managing environments — conda 4.12.0.post25+90149568 documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#removing-an-environment)
- 환경을 먼저 지워주자. 
```
conda remove --name MY-ENV --all
```

- yml 파일로부터 환경 되살리기 
[Managing environments — conda 4.12.0.post25+90149568 documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file)
```
conda env create -f MY-ENV.yml
```

## Install jupyterlab 

[Installation — JupyterLab 3.3.2 documentation](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html)
- mamba로 인스톨합시다! 
```
mamba install -c conda-forge jupyterlab
```
실행은 `jupyter lab`

## Install tensorflow 
### M1 
[Tensorflow Plugin - Metal - Apple Developer](https://developer.apple.com/metal/tensorflow-plugin/)
- 환경에 python 3.8이 깔려 있어야 한다. 
- 환경을 만들 때 python 3.8로 만들도록 하자. 

## Uninstall
- `home\{USER}\miniconda3`  디렉토리를 지우면 된다. 
- zshell을 쓴다면, 

```bash
? nano ~/.zshrc
```

- 여기에 관련 설정들이 있다. 
	- 만일 재설치 할 것이라면 그리고 환경이 바뀌지 않는다면 이걸 지울 필요가 있을까? 






 