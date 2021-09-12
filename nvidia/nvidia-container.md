# 컨테이너로 nvidia GPU 사용하기 

## Why 

- docker, podman 등의 컨테이너를 통해서 nvidia 관련 GPU 모듈을 사용한다. 
- 이 방법의 장점은 플랫폼 상에서 nvidia driver 이외 다른 것을 설치할 필요가 없다는 것이다. 
- 컨테이너란 OS 위에 OS가 올라가는 개념이라는 것을 염두해두자. 

## Which Container 

- docker가 업계 표준이었지만 최근 유료화 정책으로 인해서 podman으로 옮겨가고 있는 중 
- docker와 podman 자체는 거의 호환이 가능하기 때문에 설치 이후에 활용법 등은 편하게 쓰면 된다. 

## docker 


