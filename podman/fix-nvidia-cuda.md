# Nvidia CUDA를 써보자. 

## Why 

- WSL $\neq$ Ubuntu 


## Key Process 

### WSL 2에 맞는 CUDA 설정이 필요하다 

- Ubuntu 내에 별도의 nvidia 드라이버를 깔지 않는다. 
- CUDA만 잡아주면 된다. 

https://docs.nvidia.com/cuda/wsl-user-guide/index.html#ch02-sub03-installing-wsl2


### Podman 설치 

- 앞선 가이드에 따라서 통상적으로 포드맨을 설치한다. 

### Podman tuned for nvidia 

- 아래 가이드에 따라서 podman에 맞게 nvidia 드라이버가 활용될 수 있도록 걸어준다. 

https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#id8

### Testing Module 

#### nvidia-smi 

```shell
podman run --rm --security-opt=label=disable  --hooks-dir=/usr/share/containers/oci/hooks.d/nvidia/cuda:11.0-base nvidia-smi
```

#### nbody problem 

```shell
 podman run --env NVIDIA_DISABLE_REQUIRE=1 nvcr.io/nvidia/k8s/cuda-sample:nbody nbody -gpu -benchmark
```

#### Tensorflow 

```shell
podman run --env NVIDIA_DISABLE_REQUIRE=1 -d -it -p 127.0.0.1:8888:8888 -v $(pwd)/data:/mnt/space/ml -e GRANT_SUDO=yes -e JUPYTER_ENABLE_LAB=yes -e JUPYTER_TOKEN=1234 --name tf-devel-gpu tensorflow/tensorflow:latest-gpu-jupyter
```

