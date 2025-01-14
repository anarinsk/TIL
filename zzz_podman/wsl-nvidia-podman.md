# WSL 환경에서 Nvidia GPU를 podman과 써보자. 

## Why 
 
- WSL 2에 특화된 podman + nvidia GPU 환경을 설정하자.  


## WSL 2에 맞는 CUDA 설정

- Ubuntu 내에 별도의 nvidia 드라이버를 깔지 않는다. 
- CUDA 안 잡아도 된다. ~~CUDA만 잡아주면 된다.~~ 

## Podman 설치 

- [WSL을 위한 가이드](https://github.com/anarinsk/til/blob/master/podman/wsl-podman.md)에 따라서 podman을 설치한다. 

## nvidia-container-toolkit 
 
- 아래 가이드에 따라서 podman에 맞게 nvidia 드라이버가 활용될 수 있도록 설정을 잡아준다.
    + 아래 링크는 RHEL에 관한 가이드지만 적당히 고쳐 쓸 수 있다. 
    + 해당 디렉토리나 파일이 없는 경우는 만들면 된다.  


### Installation 

https://nvidia.github.io/nvidia-docker/

- container-toolkit을 설치할 수 있도록 리포지토리 주소를 설정하자. 

```shell
$ curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
$ curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
$ sudo apt-get update
```
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#id8


```shell
$ sudo apt install -y nvidia-container-toolkit
```

- nvidia-container-toolkit을 설치한다. 
    + 설치가 잘 안되면 위 nvidia-docker 패키지 저장소 설정 과정에서 뭔가 문제가 생긴 것이다. 

### Setups 

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
    +  `cat /etc/nvidia-container-runtime/config.toml` 내용을 직접 확인해봐도 좋겠다. 
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

- Ubuntu 20.04에서는 잘 돌고, WSL2-Ubuntu 20.04에서는 OCI 에러 발생 

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

#### GPU는 잘 잡혀 있나? 

- `localhost:8888` 혹은 `127.0.0.1:8888`로 접속해서 jupyter 아래 노트북을 하나 띄운다. 

```jupyter
# 조회 모듈 
import tensorflow as tf 
tf.config.get_visible_devices(
    device_type=None
)
```

- 아래처럼 GPU가 잡혀 있으면 설정이 제대로 들어간 것이다. 

```txt
[PhysicalDevice(name='/physical_device:CPU:0', device_type='CPU'),
 PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

- GPU를 끄고 싶다면? 

```python
# Following script is to remove GPU on jupyter 
# Initial state is achieved by "shutdown - restart" in Kernel menu 

import tensorflow as tf

physical_devices = tf.config.get_visible_devices(
    device_type=None
)

# To activate CPU only, uncomment following script 
# tf.config.set_visible_devices(physical_devices[0])
print(physical_devices)
```

- 2번 실행해야 결과를 확인할 수 있다. (이유는...)
    - GPU가 죽은 걸 확인하고 코드를 다시 실행하면 된다. 
- GPU를 다시 켜고 싶다면 커널을 다시 시작하자. 
