# Installation 
## m1 
1. [Miniconda — Conda documentation](https://docs.conda.io/en/latest/miniconda.html)
2. ~/Downloads 디렉으로 이동 
	```
	bash Miniconda3-latest-MacOSX-x86_64.sh
	```


# Command 
- 업데이트 & 업그레이드 
	- 위쪽 하나면 해주면 되는 것 같다... 
```
conda update conda --all
#conda upgrade --all
```

# Install mamba 
[mamba-org/mamba: The Fast Cross-Platform Package Manager (github.com)](https://github.com/mamba-org/mamba)

```
conda install mamba -n base -c conda-forge
```

# On env 
- general ref: [Managing environments — conda 4.12.0.post25+90149568 documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

### create
- tensorflow metal 환경은 3.8에서 돌아간다. 
- 환경이 생성되는 위치는 /Users/username/opt/envs/env-name 아래 
```
mamba create -n MY-ENV python=3.8
```

## check env 
```
mamba env list  
```

## activate / deactivate 
- 액티베이트에는 이름이 필요하지만 디액티베이트에는 필요 없다. 
```
conda activate MY-ENV
conda deactivate 
```



# Install jupyterlab 

[Installation — JupyterLab 3.3.2 documentation](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html)
- mamba로 인스톨합시다! 
```
mamba install -c conda-forge jupyterlab
```


# Install tensorflow 
## M1 
[Tensorflow Plugin - Metal - Apple Developer](https://developer.apple.com/metal/tensorflow-plugin/)
- 환경에 python 3.8이 깔려 있어야 한다. 
- 환경을 만들 때 python 3.8로 만들도록 하자. 

 