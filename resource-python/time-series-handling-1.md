# How to Handle Time Series data 

## Why 
- 보통은 날짜를 datatime으로 바꿔서 이를 직접 조작한다. 
- 하지만 이렇게 할 경우 문제가 생길 수 있다. 
  + 예를 들어 weekly 변화를 보고 싶다고 하자. 이렇게 데이터를 조작하면, 예측 등에서 예측하는 주에 문제가 생길 수 있다. 
 
## What 
- 타임시리즈를 일관되게 변형할 수 있는 방식으로 데이터를 조작하자. 


## How 
- datetime을 index로 설정 
- `pandas.resample` 방법을 통해서 데이터를 조작하자. 


## Where 
- https://jakevdp.github.io/PythonDataScienceHandbook/03.11-working-with-time-series.html
