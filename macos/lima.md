# LIMA 

## Why 

- Ubuntu on macos 
- m1에서도 잘 된다. 

## 특징 

- qemu 기반의 굉장히 가벼운 vm이다. 
- machine을 만들 떄 yaml로 어떤 vm을 만들지 컨트롤해줄 수 있다. 
- macos가 unix 기반이기 때문에 vm을 여러 개 만들어도 큰 손해가 없을 듯? 

## 실전 활용 

### 여러 개의 vm을 섞어가며 활용하기 

- 아직은 호환성으로 docker을 써야 할 수 있다. 
- 이때 vm 하나를 도커에 할애하자. 그리고 도커는 그 vm으로 쓰면 된다. 
- 나머지는 rancher desktop을 활용하면 된다. 

## Misc

### Repository 변경 

- ports 리포지토리는 카카오에 없다. 일단 그나마 빠른 lanet을 활용하자. 
    + 꼭 필요한지는 잘 모르겠다. 그냥 ports도 쓸만 한 듯. 
`sudo sed -i 's|http://ports.ubuntu.com/ubuntu-ports|http://ftp.lanet.kr/ubuntu-ports|g' /etc/apt/sources.list`


