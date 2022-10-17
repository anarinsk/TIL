# Tinytex 활용하기 

## Why 
- texlive 설치 없이, tlmgr을 활용할 방법을 모색하기 
- cross-platform 
- VS Code로 편하게 활용하자. 
- (몇 가지 잠재적인 위험은 남아 있다.)

## Installation 

### One Fits All! 
[설치하기/Tiny TeX - KTUG Wiki](http://wiki.ktug.org/wiki/wiki.php/%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0/TinyTeX)


### Tiny$\rm \TeX$

[TinyTeX - A lightweight, cross-platform, portable, and easy-to-maintain LaTeX distribution based on TeX Live - Yihui Xie | 谢益辉](https://yihui.org/tinytex/#installation)

- 텍을 쓰는 기본을 잡아준다고 생각하자. tlmgr을 활용할 수 있게 해준다. 
- 윈도우의 경우 bat 파일을 쓴다. 
	- 인스톨이 안될 때는 한번 리부트를 하자. 
- macos의 경우 
```bash
$ sudo chown -R $(whoami) /usr/local/bin
$ curl -sL "https://yihui.org/tinytex/install-bin-unix.sh" | sh
```
- 잘 깔렸는지 테스트해보자. 
```bash
tlmgr update --self --all
```

### Ko$\rm\TeX$
- 코텍을 원래 위키에 OS 별로 잘 설명이 되어 있다. 
- 우리는 $\rm\TeX$Live를 쓰는 것이 아니라, Tiny$\rm\TeX$을 쓸 예정이므로 좀 다르게 고려해보자. 
- 여기서 채택한 방법은 다음과 같다. 
	- [설치하기MacOSX/Basic TeX - KTUG Wiki](http://wiki.ktug.org/wiki/wiki.php/%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0MacOSX/BasicTeX)
- 편하게 가자. 
```bash
sudo tlmgr install collection-langkorean
``` 

### VS Code 
- LaTeX Workshop을 쓰자. 

#### 설정 손보기 
- F1 > "open settings" 검색 > `settings.json`  열기 
- 찾기로 "latex-workshop"을 찾아보자. 두 개의 헤드라인 설정을 찾아야 한다. 
	- `"latex-workshop.latex.tools"`
	- `"latex-worksop.latex.recipes"`
- 일단 둘의 설정을 아래와 같이 단순하게 놓자. 
	- PDF$\rm\LaTeX$을 쓴다고 가정 
```yaml
"latex-workshop.latex.tools" : [
    {
      "name": "pdflatex",
      "command": "pdflatex",
      "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
      ]
   }
   ],

"latex-workshop.latex.recipes": [
    {
      "name": "tex to pdf",
      "tools": [
        "pdflatex",
        "pdflatex"
      ]
    }
  ]
```

#### Unsolved 
- sync는 지원되지 않는 것 같다. 
- LaTeX Workshop 설정 