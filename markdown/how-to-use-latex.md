# How to render latex in github flavored markdown 

## Issue 

+ github 마크다운에서 latex 수식이 쉽게 표현되지 않는다.
  + mathjax로 외부에서 이미지로 렌더링한 후 붙여 넣는 방식 &rarr; 그다지 우아하지 않아! 
+ 이후의 호환성 
  + 뒤에라도 github에서 katex 등을 통해서 latex 문법을 지원하게 될 경우 수식 표현을 재활용할 수 없다. 

## Solution 1 

+ [Chome extension](https://chrome.google.com/webstore/detail/purple-pi/ingbbliecffofmmokknelnijicfcgolb/related)을 깐다. 
  + 브라우저(크롬, 엣지 크로미움 기반) 기반으로 설치하고 계정 로그인된 상태라면 깔린 클라이언트(컴퓨터)에 관계 없이 익스텐션을 동기화하므로 설치하고 잊으면 된다. 
  + 도구모음에서 숨겨 놓아도 좋다. 
+ 페이지 어딘가에 아래의 링크를 넣어둔다. 

```md
[![purple-pi](https://img.shields.io/badge/Rendered%20with-Purple%20Pi-bd00ff?style=flat-square)](https://github.com/nschloe/purple-pi?activate)
```

+ 그리고 latex을 쓴다. 

### Field testing 

[![purple-pi](https://img.shields.io/badge/Rendered%20with-Purple%20Pi-bd00ff?style=flat-square)](https://github.com/nschloe/purple-pi?activate)

Let $U$ be an open subset of the complex plane $\mathbb{C}$, and suppose the closed
disk $D$ defined as
$$
D = \bigl\\{z:|z-z_{0}|\leq r\bigr\\}
$$
is completely contained in $U$. Let $f: U\to\mathbb{C}$ be a holomorphic function, and
let $\gamma$ be the circle, oriented counterclockwise, forming the boundary of $D$.
Then for every $a$ in the interior of $D$,
$$
f(a) = \frac{1}{2\pi i} \oint _{\gamma}\frac{f(z)}{z-a} dz.
$$
