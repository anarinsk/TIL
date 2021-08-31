# Katex을 다뤄보자. 

## Problem 

- Jekyll 일반의 문제인지는 모르겠다. 
- minima 테마의 문제인지도 모르곘다. 
- Fastpage 기본 설정 아래에서 $\LaTeX$ 수식이 제대로 생성되지 않는다. 
    1. displaystyle에서 이탤릭 처리가 되지 않음 
    2. displaystyle에서 폰트 크기가 다소 작음 
    - inline에서 큰 문제가 없는 것으로 봐서는 버그? 

## Hand-on solution 

`_config.yml`에서 `math_engine`을 수정하자. 

https://anarinsk.github.io/lostineconomics-v2-1/2021/08/31/Testing-Katex.html


## Another problem 

- Katex의 경우 $\LaTeX$ 문서의 여러가지 옵션을 줄 수 있는데, 이게 불가능해진다. 
- 수식의 생성이 느라다, 고 하는데... (체험이 될 정도는 아닌 듯)