# Why 

- 텐서플로와 m1을 위한 환경을 만들어보자. 
- env를 익히는 데 큰 도움이 될 것으로 생각 

# 순서 
1. create init env 
2. install packages 
3. create yml file for env 
4. create env from yml file 

# Create init env 
- ref: [Managing environments — conda 4.12.0.post25+90149568 documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#removing-an-environment)
```
mamba create -n myenv python=3.8
```
- 이후 파이썬 버전이 업데이트될 수 있다. 

# install packages
- 우선 환경으로 진입한다. `conda activate MY-ENV`
- 패키지를 설치한다. 

## General packages 
```
mamba create matplotlib 
```

## tensorflow for m1 
https://developer.apple.com/metal/tensorflow-plugin/