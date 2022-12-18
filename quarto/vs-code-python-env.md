# qmd 내 가상환경 선택

>[!WHAT TO DO]
> - qmd 내의 파이썬 코드를 특정 가상 환경에서 컴파일하기
> - 윈도에서 발생하는 특정한 이슈 해결법 

# qmd 컴파일 

## 해결책 

F1 > python 검색 / "Python: 인터프리터 선택" > 필요한 가상 환경 선택

# Windows 커파일 에러 

커널을 찾지 못하고 에러를 띄울 때가 있다. 
에러의 원인은 conda 가상 환경에 설치된 python을 제대로 찾지 못해서 생기는 일로 jupyter와의 커널로 생각된다. 

## 해결책 

- conda 가상 환경을 그대로 써도 좋다. 
```shell
$ conda create --name for-quarto python=3.10
```
- 다만 jupyter를 깔 때는 `pip`로 설치한다. 
``` shell
$ pip install jupyter pandas matplotlib 
```

