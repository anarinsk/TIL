# Nvidia CUDA를 podman과 써보자. 

## Why 

- WSL $\neq$ Ubuntu 


## Key Process 

### WSL 2에 맞는 CUDA 설정

- Ubuntu 내에 별도의 nvidia 드라이버를 깔지 않는다. 
- CUDA만 잡아주면 된다. 

https://docs.nvidia.com/cuda/wsl-user-guide/index.html#ch02-sub03-installing-wsl2


```shell
$ wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
$ sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget https://developer.download.nvidia.com/compute/cuda/11.4.0/local_installers/cuda-repo-wsl-ubuntu-11-4-local_11.4.0-1_amd64.deb
$ sudo dpkg -i cuda-repo-wsl-ubuntu-11-4-local_11.4.0-1_amd64.deb
$ sudo apt-key add /var/cuda-repo-wsl-ubuntu-11-4-local/7fa2af80.pub
$ sudo apt-get update
$ sudo apt-get -y install cuda
```

### Podman 설치 

- [기본 가이드](https://github.com/anarinsk/til/blob/master/podman/basic.md)에 따라서 통상적으로 포드맨을 설치한다. 

#### Podman tuned for nvidia 

- 기본 아래 가이드에 따라서 podman에 맞게 nvidia 드라이버가 활용될 수 있도록 설정을 잡아준다.
    + 아래 설명이 RHEL에 관한 설명이라서 고쳐서 써야 한다. 
    + 해당 디렉토리나 파일이 없는 경우는 만들면 된다.  

https://nvidia.github.io/nvidia-docker/

```shell
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
```

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#id8


```shell
$ sudo install install -y nvidia-container-toolkit
```

- nvidia-container-toolkit을 설치한다. 
    + 설치가 잘 안되면 위 패키지 저장소 설정 과정에서 뭔가 문제가 생긴 것이다. 




### Testing Module 

- 아래 컨테이너들을 실행해보자. 

#### nvidia-smi 

```shell
$ podman run --rm --security-opt=label=disable nvidia/cuda:11.0-base nvidia-smi
```

#### nbody problem 

```shell
 $ podman run --env NVIDIA_DISABLE_REQUIRE=1 nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

#### Tensorflow 

- 토큰번호: 1234 
- 현재 디렉토리에 `data` 하위 디렉토리를 만들어야 한다. 

```shell
$ sudo podman run --env NVIDIA_DISABLE_REQUIRE=1 -d -it -p 127.0.0.1:8888:8888 -v $(pwd)/data:/mnt/space/ml -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=1234 --name tf-devel-gpu tensorflow/tensorflow:latest-gpu-jupyter
```

- 자세한 것은 [여기]를 참고 
- 테스트할 내용만 적어보자. 

GPU는 잘 잡혀 있나? 

- `localhost:8888`로 접속해서 jupyter 아래 노트북을 하나 띄운다. 

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