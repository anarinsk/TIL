# $\rm\LaTeX$ 괄호 처리 

## What 
- $\rm\LaTeX$에 필요한 각종 괄호의 렌더링 방법을 알아보자. 

## Why 
- Markdown에서는 때로는 태그 명령어와 혼동을 일으켜 렌더링이 잘 되지 않기 때문이다. 

## How

```latex
\documentclass{article}
\usepackage{mathtools}
\begin{document}
$\lparen\ \lbrack\ \lbrace\ \langle\ \lvert\ \lVert$ \quad
$\rparen\ \rbrack\ \rbrace\ \rangle\ \rvert\ \rVert$
\end{document}
```

![](https://i.stack.imgur.com/JpkXb.png)
