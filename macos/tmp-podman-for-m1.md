# Podman for M1 

## Why 

- Docker Desktop 후지다. 
- 포드맨을 써보자. 
- docker-compose와는 연동이 되어야 한다. 

## Install

- brew에서 인스톨 하자. 
    + brew 검색 창에서 'podman', 'docker-compose' 검색 
- 참고 
    + https://minwook-shin.github.io/how-to-use-docker-image-with-podman/

### podman 

- vm 활성화해주자. 
    + https://podman.io/getting-started/installation
    
    ```shell
    podman machine init
    podman machine start
    ```

    + `podman run --rm hello-world`로 테스트 해보자. 

## Be practical 

- 