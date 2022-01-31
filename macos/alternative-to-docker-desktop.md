# Alternative to Docker Desktop 

## Why 

- 유료화 정책 
- 느린 퍼포먼스 

## Docker Desktop 

- m1에서 full package를 제공한다. 
- qemu를 백엔드로 쓰지만, 프론트엔드에서는 별다른 티가 나지 않는다. 

## Way 1: Rancher Desktop 

- 언제 유료화를 할지 모르지만, 일단은 좋다. 
- brew에서 설치하자. 

### 설치

`brew install --cask rancher`

### 설정

- 특별한 건 없었다. 
- 다만 최초 인스톨에서는 "Supporting Utilities"에서 docker 등이 활성화되지 않았다. 
    + 이유를 찾지 못함 

### 활용 

- 인스톨 후 docker 바로 활용 가능 
- docker-compose를 설치해주자. `brew install docker-compose`
- 콤포즈 명령어를 별다른 이슈 없이 쓸 수 있었다. 

### Ultimate Solution?

- Kubenetes로 전환을 해야 할 듯 싶다. 
- Minikube에 대해서 차츰 공부해가자. 

## Way 2: lima + docker + docker-compose 

### Resources 

https://breezymind.com/slicon-m1-mac-lima-docker-desktop-alternative/


### 설치 

