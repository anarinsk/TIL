# Google Domains + Github Pages 

## TL; DR 

구글 도메인스로 도메인 구입하고 깃허브 페이지스랑 연결한 썰 푼다. 

## Google Domains 

- 도메인 구입 
- DNS를 다양한 방식으로 설정해줄 수 있다. 
- 나머지 설정은 거의 일반적이니 DNS만 잘 설정하면 된다. 

### DNS 
- 도메인 네임서버, 즉 구입한 도메인이 어디로 어떻게 연결되어야 하는지를 지정해준다. 
- 가장 쉬운 것은 포워딩이다. 이전에 이렇게 썼었다. 
	- lostineconomics.com을 치면 https://anarinsk.github.io/lostineconomics_quarto 로 연결되는 식이다. 
	- 포워딩의 문제는 도메인의 진정성을 담보하기 힘들다는 것이다. 
- 그래서 얘를 GitHub Pages에 내부 도메인으로 묶어보기로 했다. 

## GitHub > 도메인 인증 with TXT

- 먼저 깃헙에서 해당 도메인이 나의 소유임을 입증해야 한다. 
- Settings > Pages로 간다. 
- 여기에 해당 도메인을 인증하는 절차가 있다. 
- 얼핏 보면 내용이 복잡한데, 기본적으로 복붙이다.  

### Google Domains > DNS 설정 > "맞춤 레코드 관리"
- 새 레코드를 생성한다. 

#### TXT 인증하기 
- GitHub 도메인 인증에서 가져올 것은 "호스트이름", "데이터"이다 
- 중간에 유형은 TXT로 설정하면 된다. 
- 세팅을 하고 GitHub Pages에서 "베리파이"를 눌러주면 인증이 된다 .
- 이제 해당 도메인을 GitHub의 내부 도메인으로 쓸 수 있다.  

## Google Domain > CNAME 설정

#### CNAME 설정하기 
- 같은 방식으로 CNAME을 설정한다. 
- 호스트 이름은 가장 일반적인 차원에서는 www이다. 만일 하위 페이지를 쓰고 싶다면 별도의 이름을 지정하면 된다. 
	- `jupyterlite.anari.dev`라고 할 때 구입한 도메인은 "anari.dev"가 된다. CNAME을 통해서 앞에 jupyterlite를 연결해주면 된다. 
- 유형은 "CNAME"이다. 
- 데이터에는 포워딩될 주소의 최상위 주소를 넣어준다. 내 경우는 anarinsk.github.io
- 이 녀석 역시 포워딩이 이루어지는 데 약간의 시간이 필요하다. 
[Managing a custom domain for your GitHub Pages site - GitHub Docs](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)

```shell
$ dig WWW.EXAMPLE.COM +nostats +nocomments +nocmd
```

WWW.EXAMPLE.COM 이 원하는 주소로 잘 가고 있는지를 확인해볼 수 있다. 

```shell
$ dig www.lostineconomics.com +nostats +nocomments +nocmd
```

## GitHub Pages 설정 

- `Custom domain`을 찾자. 
- 여기서 CNAME을 설정된 페이지를 알려준다. 
- 그러면 녀석이 해당 리포의 Pages로 연결된다. 
	- www.lostineconomics.com > anarinsk.github.io/lostineconomics_quarto
	- jupyterlite.anari.dev > anarinsk.github.io/test_jupyterlite 
	