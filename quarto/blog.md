# Install blog 
## process 
- github 리포 만들기 
- 클로닝 
- 블로그 파일 생성 `quarto create-project myblog --type website:blog` 
- 블로그 튜닝 
- 퍼브리싱을 위한 설정 
- 작업 확인 
	- `quarto preview`
	- `quarto render`

## 블로그 튜닝 
- 일반적인 설정은 [여기](https://quarto.org/docs/websites/website-blog.html) 참고 

### `_quarto.yaml`
- 블로그 최상단의 리본을 꾸민다. 
- theme를 설정한다. 
- styles.css를 로드한다. 

#### styles.css 

```css
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');

@import url('https://cdn.rawgit.com/moonspam/NanumSquare/master/nanumsquare.css');
  

h1, h2, h3, h4, h5, h6 {
	font-family: 'NanumSquare' !important;
	font-weight : 600;
  }

  

p {

	font-family: 'pretendard' !important;
	font-size: 90%;
}
```

- `@import`는 웹 폰트를 로드하는 모듈 
- 각 폰트 설정 
- `!important` 뒤에서 해당 값을 변경하더라도 변경되지 않게 하는 옵션이다. 


## 퍼브리싱을 위한 설정 
> render를 하지 않으면 깃헙 등으로 보내도 설정이 적용되지 않는다!
- github pages만 알면 된다. [Quarto - Publishing Websites](https://quarto.org/docs/websites/publishing-websites.html#github-pages)
- 


