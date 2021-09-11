# 우분투에 CUDA, Podman 환경을 설정해보자. 

## Nvidia Driver 

- 기본적으로 아래 페이지 참고 

    - https://pstudio411.tistory.com/entry/Ubuntu-2004-Nvidia%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0

- 설치가 가능한지 확인하고 설치하자. 

```
# 그래픽카드 및 설치 가능한 드라이버 확인
ubuntu-drivers devices

# 현재 사용중인 그래픽카드 확인
lspci | grep -i nvidia

# 설치 
sudo ubuntu-drivers autoinstall
```

- 리부팅을 하고 나면 드라이버가 제대로 설치된 것은 프로그램 > "Additional Drivers"에서 확인할 수 있다. 