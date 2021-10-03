# Native Ubuntu Installation 

## Setting 

+ Hardware: 한성 세잔 5800H
+ Ubuntu 20.04 LTS 

## Skipped 

+ 설치 관련 자질구레한 사항 
  + 부팅 디스크 만들기 
  + 이미지 넣기 
 
## First Thing Frist 

### Update 주소 설정 

메뉴 > Software Update 선택 

- Ubuntu Software 탭에서 Downloable ... 조정 
- 여기서 얻데이트 서버를 선택할 수 있다. 

### 키보드 한영 전환 

- fcitx를 설치한다. 

```
sudo apt-get update
sudo apt-get install fcitx-hangul
```
- 나머지는 여기를 참고 하자. https://movment.tistory.com/4 

- uim도 설치하자. 

- 크로미움 기반 브라우저에서 일부 서비스에서 문제가 생긴다. 
  + 예를 들어 Twitter 

https://codechacha.com/ko/ubunutu-uim-keyboard/

### 화면 폰트 크기 전체 조정 

- --그냥 Display Settings에서 fractional setting을 150%로 쓰는 게 나은 듯도 싶다.--
- 1.2 정도가 적당한 듯.  

  ```shell
  gsettings set org.gnome.desktop.interface text-scaling-factor 1.2
  ```

## 폰트 설치 

### D2Coding Ligature & Powerline 

- D2Coding Liagature는 코딩에 필요한 글꼴, Powerline은 CLI에서 화살표 등을 제대로 나오게 하는데 필요하다. 
- D2Coding 설치하기 

```shell
apt-get install unzip
wget https://github.com/naver/d2codingfont/releases/download/VER1.3.2/D2Coding-Ver1.3.2-20180524.zip
unzip D2Coding-Ver1.3.2-20180524.zip
mkdir /usr/share/fonts/truetype/D2Coding
cp ./D2Coding/*.ttf /usr/share/fonts/truetype/D2Coding/
fc-cache -v
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

https://itlearningcenter.tistory.com/entry/%E3%80%90Ubuntu-2004-LTS%E3%80%91%EB%85%B8%ED%8A%B8%EB%B6%81-%EC%A0%84%EC%9B%90-%EA%B4%80%EB%A6%AC-%EB%8F%84%EA%B5%AC-%EC%84%A4%EC%B9%98

- TLP 설치 

```shell
sudo apt-get install tlp -y
```

- slim battery 

```shell
sudo add-apt-repository ppa:slimbook/slimbook
sudo apt-get update
sudo apt-get install slimbookbattery
```

### 절전 모드 후 먹통 현상 

- 아직 해결이 안 된 듯... 

### 뚜껑 닫았을 때 하이버네이션 모드 조정 

https://ubunlog.com/ko/como-hacer-que-ubuntu-se-suspenda-cuando-cerramos-la-tapa-del-portatil/

## podman 

### Installation 

https://github.com/anarinsk/til/blob/master/podman/ubuntu-podman.md

### nvidia setting 

https://github.com/anarinsk/til/blob/master/nvidia/nvidia-container.md

### podman + docker-compose

- 실제로 활용하는 용례 정리 

https://github.com/anarinsk/til/blob/master/podman/ubuntu-podman.md#docker-compose--podman

## Booting failure 

+ grub 부트로더의 0번이 ubuntu 실행이다. 그냥 둬서 잘 되면 OK 
+ 만일 제대로 작동하지 않는다면, 두번째 세부 설정으로 들어간다. 
  + 여기서는 linux kernel version을 선택할 수 있다. 다른 버전으로 잘 된다면 그대로 하면 된다. 
+ 내가 경우는 커널 업데이트로 해결했다. [여기](https://codechacha.com/ko/ubuntu-update-kerenl/) 참고
+ [Grub customize](https://kibua20.tistory.com/128)
