# 컨테이너로 nvidia GPU 사용하기 

## Why 

- docker, podman 등의 컨테이너를 통해서 nvidia 관련 GPU 모듈을 사용한다. 
- 이 방법의 장점은 플랫폼에 nvidia driver 이외 다른 것을 설치할 필요가 없다는 것이다. 
    + 컨테이너란 OS 위에 OS가 올라가는 개념이라는 것을 염두해두자. 

## Which Container 

- docker가 업계 표준이었지만 최근 유료화 정책으로 인해서 podman으로 옮겨가고 있는 중 
- docker와 podman 자체는 거의 호환이 가능하기 때문에 설치 이후에 활용법 등은 편하게 쓰면 된다. 

## docker 

- Windows의 경우 docker desktop을 설치하고 WSL 2와 연동하는 것으로 대충 다 해결된다.
    + nvidia docker를 별도로 설치하지 않아도 된다. 
    + WSL 2와 연동될 경우 안에 사실상 3개의 컨테이너를 돌리고 있는 셈이다. 
- Linux의 경우 docker CE를 설치한다. 
    + nvidia 도커 설치 여부는 확인이 필요하다. 

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
    + 자세한 설명을 생략하도록 한다. 
- 기본적으로 WSL 2, native ubuntu에서건 활용법은 같다. 
    + 다만 podman 설치를 하는 것에서 차이가 있다. 

### nvidia-container-toolkit

- nvidia gpu를 컨테이너와 연결해주는 도구  
- 아래 가이드에 따라서 podman에 맞게 nvidia 드라이버가 활용될 수 있도록 설정을 잡아준다.
    + 아래 링크는 RHEL에 관한 가이드지만 적당히 고쳐 쓸 수 있다. 
    + 해당 디렉토리나 파일이 없는 경우는 만들면 된다.  

#### Setup apt for nvidia-container-toolkit 

https://nvidia.github.io/nvidia-docker/

```shell
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
```

### From toolkit to podman 

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#id8


```shell
$ sudo apt install -y nvidia-container-toolkit
```

- nvidia-container-toolkit을 설치한다. 
    + 설치가 잘 안되면 위 nvidia-docker 패키지 저장소 설정 과정에서 뭔가 문제가 생긴 것이다. 

- `cat /usr/share/containers/oci/hooks.d/oci-nvidia-hook.json` 파일이 존재하는지 확인해 본다. 없다면 하나 만들도록 하자. 

```shell
$ sudo mkdir -p /usr/share/containers/oci/hooks.d
$ sudo nano /usr/share/containers/oci/hooks.d/oci-nvidia-hook.json
```

- json 파일은 아래와 같다. 

```json
{
    "version": "1.0.0",
    "hook": {
        "path": "/usr/bin/nvidia-container-toolkit",
        "args": ["nvidia-container-toolkit", "prestart"],
        "env": [
            "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
        ]
    },
    "when": {
        "always": true,
        "commands": [".*"]
    },
    "stages": ["prestart"]
}
```

- podman 실행을 위해 설정을 아래와 같이 변경한다. 
    + `config.toml` 파일을 직접 열어 수정해도 된다. 
- cat 명령어로 확인해보자. 

```shell
$ sudo sed -i 's/^#no-cgroups = false/no-cgroups = true/;' /etc/nvidia-container-runtime/config.toml
$ cat /etc/nvidia-container-runtime/config.toml
```

## Testing Module 

- 아래 컨테이너들을 실행해보자. 
- 제대로 실행되었다면 nvidia-smi가 실행될 것이다. 
    + WSL 내에 CUDA를 설치한 적이 없다는 사실을 기억하자. 이 프로그램은 컨테이너 내에서 돌아가는 것이다.  
- 보다 많은 사례는 다음을 참고하자. 
    + https://hub.docker.com/r/nvidia/samples/tags

### nvidia-smi 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.0-base nvidia-smi
```

- 테스트 기기에 맞는 최신 버전을 끌어와보자. 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.4.1-base-ubuntu20.04 nvidia-smi
```

### FP16 GEMM

- 원래 한참 반응이 없는 것이 정상이다. 
- Ubuntu native에서는 제대로 실행되었지만, WSL 2에서 제대로 실행되지 않았다. 

```shell
podman run --rm --security-opt=label=disable \
     --hooks-dir=/usr/share/containers/oci/hooks.d/ \
     --cap-add SYS_ADMIN nvidia/samples:dcgmproftester-2.0.10-cuda11.0-ubuntu18.04 \
     --no-dcgm-validation -t 1004 -d 30
```

### nbody problem 

```shell
podman run --env NVIDIA_DISABLE_REQUIRE=1 nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

### Tensorflow 

- 토큰번호: 1234 
- 현재 디렉토리에 `data` 하위 디렉토리를 만들어야 한다. 

```shell
podman run --env NVIDIA_DISABLE_REQUIRE=1 -d -it -p 127.0.0.1:8888:8888 -v $(pwd)/data:/mnt/space/ml -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=1234 --name tf-devel-gpu tensorflow/tensorflow:latest-gpu-jupyter
```

- 자세한 것은 [여기]를 참고 
- 테스트할 내용만 적어보자. 

#### GPU는 잘 잡혀 있나? 

- `localhost:8888` 혹은 `127.0.0.1:8888`로 접속해서 jupyter 아래 노트북을 하나 띄운다. 
- 활성화된 디바이스 보기 

```python
import tensorflow as tf
tf.config.get_visible_devices(
    device_type=None
)
```

- 아래와 같이 GPU가 잡혀 있으면 설정이 제대로 들어간 것이다. 

```txt
[PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU'),
 PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

- gpu 비활성화 하기 

```python
import tensorflow as tf

physical_devices = tf.config.get_visible_devices(
    device_type=None
)

# CPU Only 
# tf.config.set_visible_devices(physical_devices[0])
# Initial state is achieved by "shutdown - restart" in Kernel menu 
print(physical_devices)
```

- GPU 활성/비활성을 오가는 방법 
    + 최초 활성화된 상태 (위의 방법으로 확인 가능)
    + 위의 코드를 위쪽에 넣고 `# tf.config...` 주석을 해제한다.
    + GPU가 제외되었음을 확인할 수 있다. 이 상태에서 해당 셀 아래 실행을 통해 GPU를 제외한 작업을 지시할 수 있다. 
    + 만일 다시 GPU를 활성화하고 싶으면 kernel 메뉴에서 restart를 선택하면 된다.   
