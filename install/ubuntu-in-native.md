# Native Ubuntu Installation 

## Setting 

+ Hardware: 한성 세잔 5800H
+ Ubuntu 20.04 LTS 


## Skipped 

+ 설치 관련 자질구레한 사항 
  + 부팅 디스크 만들기 
  + 이미지 넣기 

## Booting failure 

+ grub 부트로더의 0번이 ubuntu 실행이다. 그냥 둬서 잘 되면 OK 
+ 만일 제대로 작동하지 않는다면, 두번째 세부 설정으로 들어간다. 
  + 여기서는 linux kernel version을 선택할 수 있다. 다른 버전으로 잘 된다면 그대로 하면 된다. 
+ 내가 경우는 커널 업데이트로 해결했다. [여기](https://codechacha.com/ko/ubuntu-update-kerenl/) 참고 

## 한영 전환 

+ https://codechacha.com/ko/ubunutu-uim-keyboard/

## Docker 설치 

https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
