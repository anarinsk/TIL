# Native Ubuntu Installation 

## Setting 

+ Hardware: 한성 세잔 5800H
+ Ubuntu 20.04 LTS 

## Unsolved 

+ nvidia driver problem 
  + 메인 노트북 화면이 죽고 외부 디스플레이만 활성화되는 문제 

## Skipped 

+ 설치 관련 자질구레한 사항 
  + 부팅 디스크 만들기 
  + 이미지 넣기 
 
 ## Linux Kernel Update 
 
 https://blog.daum.net/kssoft/151
 

## Booting failure 

+ grub 부트로더의 0번이 ubuntu 실행이다. 그냥 둬서 잘 되면 OK 
+ 만일 제대로 작동하지 않는다면, 두번째 세부 설정으로 들어간다. 
  + 여기서는 linux kernel version을 선택할 수 있다. 다른 버전으로 잘 된다면 그대로 하면 된다. 
+ 내가 경우는 커널 업데이트로 해결했다. [여기](https://codechacha.com/ko/ubuntu-update-kerenl/) 참고
+ [Grub customize](https://kibua20.tistory.com/128)

## 폰트 설정 

### D2Coding Ligature & Powerline 

https://syssurr.tistory.com/270https://proni.tistory.com/entry/%F0%9F%90%A7-Ubuntu-D2Coding-%ED%8F%B0%ED%8A%B8-%EC%84%A4%EC%B9%98-%EB%B0%8F-Powerline-symbol-%EC%84%A4%EC%A0%95

- D2Coding Liagature는 코딩에 필요한 글꼴, Powerline은 CLI에서 화살표 등을 제대로 나오게 하는데 필요하다. 

### Nanum Font 설치 

https://syssurr.tistory.com/270 

- 아래 터미널에서 설치하는 방법으로 하자.  

## 한영 전환 

+ https://codechacha.com/ko/ubunutu-uim-keyboard/

## Docker

### 설치 

+ [도커 설치](https://docs.docker.com/engine/install/ubuntu/)
+ [도커 콤포즈 설치](https://docs.docker.com/compose/install/)

### 운용



