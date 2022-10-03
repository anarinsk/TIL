- 일상적인 워크플로우를 적어 본다. 

## envronment

### creation, list, remove, clone 
```bash
$ conda create --name(-n) {YOUR-ENV-CREATING} python=3.8
$ conda env list 
$ conda env remove --name {YOUR-ENV-DELETING}
$ conda create --name {YOUR-ENV-CREATING} --clone {YOUR-ENV-CLONED}
```
- julia도 가능한 듯. 
	- arm64에서는 가능하지 않았다... 

### Install 
```bash
$ conda install {YOUR-PACKAGE-INSTALLING}(=x.x.x)
$ conda remove {YOUR-PACKAGE-REMOVING}
```



