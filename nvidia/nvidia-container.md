# 컨테이너로 nvidia GPU 사용하기 

## Why 

- docker, podman 등의 컨테이너를 통해서 nvidia 관련 GPU 모듈을 사용한다. 
- 이 방법의 장점은 플랫폼 상에서 nvidia driver 이외 다른 것을 설치할 필요가 없다는 것이다. 
- 컨테이너란 OS 위에 OS가 올라가는 개념이라는 것을 염두해두자. 

## Which Container 

- docker가 업계 표준이었지만 최근 유료화 정책으로 인해서 podman으로 옮겨가고 있는 중 
- docker와 podman 자체는 거의 호환이 가능하기 때문에 설치 이후에 활용법 등은 편하게 쓰면 된다. 

## docker 

- Windows의 경우 docker desktop을 설치하고 WSL 2와 연동하는 것으로 대충 다 해결된다. 
    + WSL 2와 연동될 경우 안에 사실상 3개의 컨테이너를 돌리고 있는 셈이다. 

- Linux의 경우 docker CE를 설치한다. 

### Test run 

- 아래는 cuda 설치를 확인할 수 있는 docker다. 
  + 드라이버 버전 인식에 에러가 종종 있는 것 같다. 아래와 같이 버전 체크 없이 돌리자; `--env NVIDIA_DISABLE_REQUIRE=1` 
  + 에러 없이 뭔가 돌렸다는 메시지를 받으면 잘 설치된 것이다. 

```shell
docker run --gpus=all --env NVIDIA_DISABLE_REQUIRE=1 nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

- 잘 돌아간 예시화면 

```shell
$ docker run --gpus all nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
Run "nbody -benchmark [-numbodies=<numBodies>]" to measure performance.
        -fullscreen       (run n-body simulation in fullscreen mode)
        -fp64             (use double precision floating point values for simulation)
        -hostmem          (stores simulation data in host memory)
        -benchmark        (run benchmark to measure performance)
        -numbodies=<N>    (number of bodies (>= 1) to run in simulation)
        -device=<d>       (where d=0,1,2.... for the CUDA device to use)
        -numdevices=<i>   (where i=(number of CUDA devices > 0) to use for simulation)
        -compare          (compares simulation results running once on the default GPU and once on the CPU)
        -cpu              (run n-body simulation on the CPU)
        -tipsy=<file.bin> (load a tipsy model file for simulation)

NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.

> Windowed mode
> Simulation data stored in video memory
> Single precision floating point simulation
> 1 Devices used for simulation
GPU Device 0: "GeForce GTX 1070" with compute capability 6.1

> Compute 6.1 CUDA device: [GeForce GTX 1070]
15360 bodies, total time for 10 iterations: 11.949 ms
= 197.446 billion interactions per second
= 3948.925 single-precision GFLOP/s at 20 flops per interaction
```

### Tensorflow W/ Jupyter in DOCKER 

- Docker를 통해서 Tensorflow를 Jupyter로 접근하는 법을 알아보자. 

```shell
docker run --gpus=all --env NVIDIA_DISABLE_REQUIRE=1 -d -it -p 127.0.0.1:8888:8888 -v $(pwd)/data:/mnt/space/ml -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=YOUR_NUMBERS --name tf-devel-gpu tensorflow/tensorflow:latest-gpu-jupyter
```

- `gpus=all`, `--env NVIDIA_DISABLE_REQUIRE=1`는 gpu 구동을 위한 옵션이다. 
- 나머지는 도커 실행 옵션이다. 
  - `d`: detached mode 
  - `it`: 
  - `p`: port forwarding 
  - `v`: Volume creating 
  - `-e`
    - `GRANT_SUDO=yes`: sudo 부여 
    - `JUPYTER_ENABLE_LAB=yes`: lab을 활성화
    - `JUPYTER_TOKEN=YOUR_NUMBERS`: `YOUR_NUMBERS`로 토큰(주피터 비번) 지정  

### How to check 

- tf 노트북에서 아래의 명령을 실행해 본다. 

```python
import tensorflow
from tensorflow.python.client import device_lib
tensorflow.config.list_physical_devices('GPU')
print(device_lib.list_local_devices())
```

- gpu가 잘 잡혔는지 확인해볼 수 있다. 
- gpu 옵션을 끄고 싶다면? 

```python
import os
os.environ["CUDA_VISIBLE_DEVICES"] = "-1"
```

- 노트북 맨 위에 올리자. 전환이 필요하면 커널 리로딩을 해야 한다. 
- "0"은 GPU 1개 일 때 해당 GPU를 쓴다는 이야기다. "-1"은 GPU를 죽인다는 뜻. 

## podman 

- podman은 docker를 대체할 수 있는 컨테이터 환경이다. 
- 자세한 설명을 생략하도록 한다. 
- 기본적으로 WSL 2, native ubuntu에서건 활용법은 같다. 
    + 다만 podman 설치를 하는 것에서 차이가 있다. 

### Installation 

