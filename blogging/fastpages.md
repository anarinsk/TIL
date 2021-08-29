# Fastpages 블로그 유지보수 하기 

## Upgrade 

- Fastpages는 업그레이드가 편리하다. 
- Github 내에서 issue를 발행한 후 여기서 UPGRADE 항목을 택한다. 
- 문제가 없으면 자기가 블로그를 서비스하고 있는 깃허브 리포의 관련 항목이 잘 업데이트 된다. 

### 주의사항 
- 간혹 자기 소개 등 일부 특화 페이지가 리셋되는 경우가 있다. 

## Styling 

- Fastpages는 Jekyll의 `minima` 테마에 기반한다. 
- 해당 테마의 css는 `_sass/minima`에 모여 있다. 

### 폰트 변경 

- `custom-styles.scss`로 간다. 
- 폰트 로딩에서 해당 폰트를 로드한다. 

```css
// font loading 
@import url('https://fonts.googleapis.com/css?family=Nanum+Gothic');
@import url('https://fonts.googleapis.com/css?family=Sunflower:500');
```

- 본문의 사용할 글꼴과 기본 사이즈를 지정해준다. 

```css
// Add your styles below
// make non-headings slightly lighter
.post-content p, .post-content li {   
   font-family: "Nanum Gothic", normal;
   font-size: 15px;
   color: #515151;
   font-weight: 400;
}
```

- 제목의 글꼴을 지정해준다. 

```css
h1, h2, h3, h4, h5, h6{
   font-family:"Sunflower", normal; 
}
```

### Inline coding size 

- 인라인 코딩, 즉 ` ` `로 인라인에서 설정하는 내용의 글자 크기가 마음에 들지 않았다. 
- 하일라이팅에 되어 있으므로 해당 하일라이팅 스타일을 찾아보자. 이는 `fastpages-dracula-highlight.scss`에서 찾을 수 있다. `18px`를 `13px`로 교체했다. 

```css
p code{
  font-size: 13px;
}
```

