# Native Ubuntu Installation 

## Setting 

+ Hardware: 한성 세잔 5800H
+ Ubuntu 21.10 Desktop 

## Skipped 

+ 설치 관련 자질구레한 사항 
  + 부팅 디스크 만들기 
  + 이미지 넣기 
 
## First Thing Frist 

### Update 주소 설정 

메뉴 > Software Update 선택 

- Ubuntu Software 탭에서 Downloable ... 조정 
- 여기서 업데이트 서버를 선택할 수 있다. 
    - kakao mirror 서버 정도가 좋겠다. 

### 키보드 한영 전환 

- ~~fcitx를 설치한다.~~
- 그냥 uim을 설치하도록 하자! 

```
sudo apt-get updat1e
sudo apt-get install fcitx-hangul
```
- 나머지는 여기를 참고 하자. https://movment.tistory.com/4 

- uim을 설치하자. 

- fcitx의 경우 크로미움 기반 브라우저에서 일부 서비스에서 문제가 생긴다. 
  + 예를 들어 Twitter 

https://codechacha.com/ko/ubunutu-uim-keyboard/

### 화면 폰트 크기 전체 조정 

- 그냥 Display Settings에서 fractional setting을 150%로 쓰는 게 나은 듯도 싶다.
- 125% 정도가 적당한 듯.  

  ```shell
  gsettings set org.gnome.desktop.interface text-scaling-factor 1.2
  ```

## 폰트 설치 

### D2Coding Ligature & Powerline 

- D2Coding Liagature는 코딩에 필요한 글꼴, Powerline은 CLI에서 화살표 등을 제대로 나오게 하는데 필요하다. 
- D2Coding 설치하기 

```shell
sudo apt-get install unzip
wget https://github.com/naver/d2codingfont/releases/download/VER1.3.2/D2Coding-Ver1.3.2-20180524.zip
unzip D2Coding-Ver1.3.2-20180524.zip
sudo mkdir /usr/share/fonts/truetype/D2Coding
sudo cp ./D2Coding/*.ttf /usr/share/fonts/truetype/D2Coding/
sudo fc-cache -v
```

- `fc-cache -f -v` 폰트 인식 
- `fc-list | grep "D2Coding"` 설치 확인 
- 다운로드 및 zip 푼 디렉토리에서 `rm -rf D2Coding*` 다운로드 파일 지우기 

### Nanum Font 설치 

https://syssurr.tistory.com/270 


```shell
sudo apt-get install fonts-nanum*
sudo fc-cache -fv
```

## Misc 

### 전원 관리 

- 이번 버전에서 나타났던 하이버네이션 이상 현상은 없는 듯 싶다. 

## podman 

### Installation 

https://github.com/anarinsk/til/blob/master/podman/ubuntu-podman.md

### nvidia setting 

https://github.com/anarinsk/til/blob/master/nvidia/nvidia-container.md

### podman + docker-compose

- 실제로 활용하는 용례 정리 

https://github.com/anarinsk/til/blob/master/podman/ubuntu-podman.md#docker-compose--podman