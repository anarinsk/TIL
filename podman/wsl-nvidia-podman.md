# WSL 환경에서 Nvidia GPU를 podman과 써보자. 

## Why 
 
- WSL 2에 특화된 podman + nvidia GPU 환경을 설정하자.  


## WSL 2에 맞는 CUDA 설정

- Ubuntu 내에 별도의 nvidia 드라이버를 깔지 않는다. 
- CUDA 안 잡아도 된다. ~~CUDA만 잡아주면 된다.~~ 

## Podman 설치 

- [기본 가이드](https://github.com/anarinsk/til/blob/master/podman/basic.md)에 따라서 WSL에 적합하게 podman을 설치한다. 

## nvidia docker 2

- nvidia docker 2를 설치한다. 
    + 이름은 도커지만 컨테이너 환경 일반에 적용 가능하다. 
- 기본 아래 가이드에 따라서 podman에 맞게 nvidia 드라이버가 활용될 수 있도록 설정을 잡아준다.
    + 아래 링크는 RHEL에 관한 가이드지만 적당히 고쳐 쓸 수 있다. 
    + 해당 디렉토리나 파일이 없는 경우는 만들면 된다.  


### Install nvidia-docker 

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

- podman 실행을 위해 설정을 아래와 같이 변경한다. 
    + `config.toml` 파일을 직접 열어 수정해도 된다. 

```shell
sudo sed -i 's/^#no-cgroups = false/no-cgroups = true/;' /etc/nvidia-container-runtime/config.toml
```

## Testing Module 

- 아래 컨테이너들을 실행해보자. 

### nvidia-smi 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.0-base nvidia-smi
```

- 테스트 기기에 맞는 최신 버전을 끌어와보자. 

```shell
podman run --rm --security-opt=label=disable nvidia/cuda:11.4.1-base-ubuntu20.04 nvidia-smi
```

### FP16 GEMM

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
