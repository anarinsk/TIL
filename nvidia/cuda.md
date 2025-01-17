# CUDA의 용법을 알아보자! 

## Why 

- CUDA의 설치 및 본격적인 작업을 위한 사전 설정을 알아보자. 

## Preliminary 

- CUDA를 설치한다는 의미는 플랫폼 별로 로컬로 설치한다는 뜻이다. 
- 만일 컨테이너 등을 통해서 별도의 OS를 얹는다면, 로컬에 CUDA를 설치할 필요는 없다. 
- 로컬 머신에 드라이버를 설정하는 것과는 다르다. 
    + 로컬이 드리이버를 통해 컨테이너의 하드웨어가 제어되기 때문이다. 
    + 윈도에서 컨테이너를 이용할 경우 윈도 드라이버를 제대로 깔아야 한다. 리눅스에서도 마찬가지 

## Install 

- 인스톨하는 방법은 쉽다. 
- 아래 링크에서 각기 맞는 경우를 찾아서 깔면 된다. 
- 단 Linux의 runflie로 깔끔하게 깔아주자. 

### Choose your platform 

https://developer.nvidia.com/cuda-downloads

### Documentation 

https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html#introduction

## Sample 

- 테스트하는 용도다. 
- 빌드를 한 후에 실행하는 개념이다. 

```shell
$ cuda-install-samples-11.4.sh ~
$ cd ~/NVIDIA_CUDA-11.4_Samples/5_Simulations/nbody
$ make
$ ./nbody
```

- 별 문제가 없으면 잘 실행될 것이다. 
