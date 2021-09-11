# 우분투에 CUDA, Podman 환경을 설정해보자. 

## Nvidia Driver 

- 기본적으로 아래 페이지 참고 

    - https://pstudio411.tistory.com/entry/Ubuntu-2004-Nvidia%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0

- 설치가 가능한지 확인하고 설치하자. 

```shell
# 그래픽카드 및 설치 가능한 드라이버 확인
ubuntu-drivers devices

# 현재 사용중인 그래픽카드 확인
lspci | grep -i nvidia

# 설치 
sudo ubuntu-drivers autoinstall
```

- 리부팅을 하고 나면 드라이버가 제대로 설치된 것은 프로그램 > "Additional Drivers"에서 확인할 수 있다. 
- 혹은 터미널에서 `nvidia-smi`를 실행하자. 

## podman + nvidia docker 2 

- 만일 컨테이너를 통해서 CUDA를 쓴다면 굳이 로컬에 CUDA를 설치할 필요가 없다. 
    - CUDA 등의 세부 설정이 귀찮다면 podman꽈 nvidia docker 2를 설치하도록 하자. 
- 아울러 모든 과정이 WSL 내에서 진행되는 것과 다를 바 없다! 컨테이너가 좋다는 게 이런게 아닐까? 

## Install podman 

```shell
1> cat /etc/lsb-release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.2 LTS"

2> export VERSION_ID="20.04"

> echo "deb https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /" | sudo tee /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list
> curl -L https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/Release.key | sudo apt-key add -
> sudo apt-get update
> sudo apt-get -y upgrade
> sudo apt-get -y install podman
```

1. Ubuntu 버전을 확인한다. 
2. 해당 버전을 세팅한다. 

## nvidia docker 2 

- 엔비디아 독커는 엔비디아 드라이버와 도커/컨테이너가 소통하도록 하는 역할을 한다. 

https://nvidia.github.io/nvidia-docker/

```shell
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
```

### nvidia docker to podman 

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#id8


```shell
$ sudo apt install -y nvidia-container-toolkit
```

- nvidia-container-toolkit을 설치한다. 
    + 설치가 잘 안되면 위 nvidia-docker 패키지 저장소 설정 과정에서 뭔가 문제가 생긴 것이다. 


- `cat /usr/share/containers/oci/hooks.d/oci-nvidia-hook.json` 파일이 존재하는지 확인해 본다. 없다면 하나 만들도록 하자. 

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

- podman 실행을 위해 설정 변경 

```shell
sudo sed -i 's/^#no-cgroups = false/no-cgroups = true/;' /etc/nvidia-container-runtime/config.toml
```

### Testing Module 

- 아래 컨테이너들을 실행해보자. 

#### nvidia-smi 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.0-base nvidia-smi
```

- 테스트 기기에 맞는 최신 버전을 끌어와보자. 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.4.1-base-ubuntu20.04 nvidia-smi
```

#### FP16 GEMM

```shell
podman run --rm --security-opt=label=disable \
     --hooks-dir=/usr/share/containers/oci/hooks.d/ \
     --cap-add SYS_ADMIN nvidia/samples:dcgmproftester-2.0.10-cuda11.0-ubuntu18.04 \
     --no-dcgm-validation -t 1004 -d 30
```

#### nbody problem 

```shell
 podman run --env NVIDIA_DISABLE_REQUIRE=1 nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

#### Tensorflow 

- 토큰번호: 1234 
- 현재 디렉토리에 `data` 하위 디렉토리를 만들어야 한다. 

```shell
sudo podman run --env NVIDIA_DISABLE_REQUIRE=1 -d -it -p 127.0.0.1:8888:8888 -v $(pwd)/data:/mnt/space/ml -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=1234 --name tf-devel-gpu tensorflow/tensorflow:latest-gpu-jupyter
```

- 자세한 것은 [여기]를 참고 
- 테스트할 내용만 적어보자. 

GPU는 잘 잡혀 있나? 

- `localhost:8888` 혹은 `127.0.0.1:8888`로 접속해서 jupyter 아래 노트북을 하나 띄운다. 

```jupyter
import tensorflow
from tensorflow.python.client import device_lib
tensorflow.config.list_physical_devices('GPU')
print(device_lib.list_local_devices())
```

- 아래와 같이 GPU가 잡혀 있으면 설정이 제대로 들어간 것이다. 

```txt
[name: "/device:CPU:0"
device_type: "CPU"
memory_limit: 268435456
locality {
}
incarnation: 11577691364291760396
, name: "/device:GPU:0"
device_type: "GPU"
memory_limit: 5721423872
locality {
  bus_id: 1
  links {
  }
}
incarnation: 8317357823441426046
physical_device_desc: "device: 0, name: NVIDIA GeForce RTX 3070 Laptop GPU, pci bus id: 0000:01:00.0, compute capability: 8.6"
]
```

## CUDA 설치 

https://developer.nvidia.com/cuda-toolkit-archive

- 여기서 필요한 조건을 선택하면 인스톨 방법을 알려준다. 
- 마지막에 runfile로 실행하도록 하자. 