# Recommendation for Font 

## VS Code 

VS Code 등의 에디터에서 쓸 한글 폰트 

- 파일 -> 기본설정 -> 설정 [사용자] -> (검색에서) font 
- `Editor: Font Family`
	- "Hack Nerd Font", "D2Coding ligature"
	- 멀티 폰트를 지원함으로 이렇게 설정하면 되겠다. 

- D2 코딩 with ligature + Nerd 
	- [kelvinks/D2Coding_Nerd: D2Coding 1.3.2 Version Nerd Patch (github.com)](https://github.com/kelvinks/D2Coding_Nerd)
	- 일부 특수 문자가 깨지는 단점이 존재 
- Hack Nerd Patched 
	- [LINK](https://www.nerdfonts.com/font-downloads)에서 Hack을 찾아서 다운로드
- 다중 폰트를 지원 

## Windows Terminal 
- 다중폰트를 지원하지 않는다. D2Coding ligature를 써도 좋지만 일부 깨짐이 발견 
- Hack Nerd Patched를 쓰도록 하자. 
- 폰트를 설치한 후 WT 설정 → PS 설정 → 모양 안에서 앞서 설치한 폰트

## Blogging 

- 본문: 프리텐다드 [Pretendard (tistory.com)](https://cactus.tistory.com/306)
- h1-h6: 나눔고딕스퀘어 [네이버 글꼴 모음 (naver.com)](https://hangeul.naver.com/font)
- 코드: D2코딩 

### 블로그 적용 폰트 세팅 
- css에서 `@import`를 통해서 적용 
- [lostineconomics.com - (anarinsk.github.io)](https://anarinsk.github.io/lostineconomics_quarto/) 에 적용된 폰트 `anari-custom.css`

```css
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css'); 
@import url('https://cdn.rawgit.com/moonspam/NanumSquare/master/nanumsquare.css'); 
@import url("https://cdn.jsdelivr.net/gh/wan2land/d2coding/d2coding-ligature-subset.css");
```

## Jupyter 
- 복잡한 폰트 설정이 있지만, 그냥 패키지를 깔도록 하자! 
- `pip install koreanize-matplotlib`