# LIMA 

## Why 

- Ubuntu on macos 
- m1에서도 잘 된다. 

## Repository 변경 

- ports 리포지토리는 카카오에 없다. 일단 그나마 빠른 lanet을 활용하자. 

`sudo sed -i 's|http://ports.ubuntu.com/ubuntu-ports|http://ftp.lanet.kr/ubuntu-ports|g' /etc/apt/sources.list`

