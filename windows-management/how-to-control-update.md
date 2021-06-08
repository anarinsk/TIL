# 문제 

- 윈도우 업데이트 시 개발자 버전을 쓰면 사용 환경에 따라서 많이 불안해 진다. 
  + 21390 버전에서 Hello update, net(Realtek) update를 하면 바로 다운되는 현상 발생 
- 이럴 때 업데이트를 멈추는 것 말고 이를 통제할 수 있으면 좋을 것 같다. 


# 해결 

WUMT
http://forum.ru-board.com/topic.cgi?forum=5&topic=48142#2 

- 설치가 필요하지 않다. 윈도 업데이트를 통제할 수 있다. 

## 활용사례 

- 일단 윈도 설정에서 업데이트를 멈춰 놓는다.
- WUMT에서 "업데이트" 아이콘을 누르면 어떤 업데이트 및 상태를 있는지 볼 수 있다. 

![](https://github.com/anarinsk/til/blob/master/windows-management/image.png)

- 문제가 있는 업데이트를 선택한 후 휴지통으로 보낸다.
  + Hidden 항목으로 간다. 
- 업데이트를 재개하면, 해당 업데이트는 목록에서 알아서 제외된다. 
- 설치를 원할 경우 스크린 샷의 아이콘의 설치 아이콘을 통해 설치가 가능하다. 


# Reference 

https://zkim0115.tistory.com/966
