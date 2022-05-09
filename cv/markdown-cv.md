# Why 
- cv를 만드는 여러가지 방법이 있지만 외관보다 더 신경 쓰이는 것이 유지보수다. 
	- latex을 쓰든 rmarkdown+rstudio를 쓰든 뭔가 별도의 도구가 필요하다. 
	- vs code 만으로 간단히 빌드하기를 소망한다. 
- 간편한 유지 보수와 호스팅을 동시에 달성하는 방법으로 markdown-cv를 고려하자. 

## Working logic 
- github는 기본 블로깅 툴로 jekyll을 지원한다. 
	- 이는 적절한 설정 파일을 밀어 넣으면 얘가 md를 html로 빌드해준다는 이야기 
	- 파일 이름이 index.md일 경우에는 github pages의 대문으로도 기능한다. 
	- 최소한으로 게으르게 css를 손봐서 쓸만한 cv를 만들도록 하자. 

# Missions 
1. LaTeX이 포함되게 한다. 
2. 폰트 변경 및 글자 크기 변동을 가능하게 한다. 

# How to build 

## fork repo 
[elipapa/markdown-cv: a simple template to write your CV in a readable markdown file and use CSS to publish/print it. (github.com)](https://github.com/elipapa/markdown-cv)

**forked repo** 
[anarinsk/markdown-cv: a simple template to write your CV in a readable markdown file and use CSS to publish/print it. (github.com)](https://github.com/anarinsk/markdown-cv)

## modification 

- `index.md`: cv 내용이다. 
-  `_config.yml`: 빌드를 위한 yml 설정 
- `_layout/cv.html`: 헤드를 손봐야 한다. 
- `media`: 폴더 안에 css가 들어 있다. 커스터마이즈가 필요하다. 

## `_config.yml`

```yml
markdown:   kramdown
kramdown:
  math_engine: katex
style:  davewhipp
```
- `kramdown`: 크램다운에 매스 엔진을 활성화해주는 부분이다. 
- `style`: css 중에서 어떤 스타일을 쓸 것인지 결정한다. 
	- devewhipp, kjhealy 두 개가 있다. 전자를 쓸 것이다. 

## `_layout/cv.html`
```html
<link href="media/styles.css" type="text/css" rel="stylesheet" media="screen">

<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.css" integrity="sha384-yFRtMMDnQtDRO8rLpMIKrtPCD5jdktao2TV19YiZYWMDkUR5GQZR/NOVTdquEx1j" crossorigin="anonymous">

<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/katex.min.js" integrity="sha384-9Nhn55MVVN0/4OFx7EE5kpFBPsEMZxKTCnA+4fqDmg12eCTqGi6+BB2LjY8brQxJ" crossorigin="anonymous"></script>

<script defer src="https://cdn.jsdelivr.net/npm/katex@0.10.2/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
```
- 이 추가 라인은 `<head>` 태그 안에 넣어주자. 
- 뒤의 세 라인은 katex의 math engine을 로드한다. 
- 첫 라인은 특화된 css를 로딩하기 위한 설정이다. 

## media 

### `daveshipp-.css`
- 어떤 스타일을 쓰는지에 따라서 고쳐야 하는 부분이 다르다. 
- 끝이 `-print`로 끝나는 것과 `-screen`으로 끝나는 것이 있다. 전자는 인쇄용, 후자는 화면 열람용이다. 둘 다 대동소이하다. 
- 제목이 너무 커서 h1 사이즈를 수정했다. 원래 `3em`으로 설정된 것을 `150%` 수정 

```css
h1 {
	text-align: left;
	font-size: 150%;
	line-height: 1em;
	position: relative;
	left: 25%;
}

```

### `styles.css 
- 블로그에 썼던 스타일을 그대로 가져왔다. 
- 폰트 설정하는 것 이외에는 하는 일이 없다. 

```css
/* css styles */
/* @import url('https://fonts.googleapis.com/css2?family=Nanum+Gothic&display=swap'); */
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
@import url('https://cdn.rawgit.com/moonspam/NanumSquare/master/nanumsquare.css');
@import url("https://cdn.jsdelivr.net/gh/wan2land/d2coding/d2coding-ligature-subset.css");

h1, h2, h3, h4, h5, h6 {
    font-family: 'NanumSquare' !important;
    font-weight : 600;
  }

ul, li, ol, a{
    font-family: 'pretendard' !important;
    font-size:95%;
   }

p {
    font-family: 'pretendard' !important;
    font-size: 100%;
    font-weight: 400; 
}

.category {
  font-size: 90%;
}

.sourceCode {
  font-family: 'D2Coding', monospace !important;
  font-size: 95%;
}
```

# Output 
[Junsok Huhh's CV | CV (anarinsk.github.io)](https://anarinsk.github.io/markdown-cv/)