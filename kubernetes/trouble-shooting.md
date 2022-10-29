# 문제 해결 

## yaml이 vs code에서 보기 흉할 때 

[R, Python 분석과 프로그래밍의 친구 (by R Friend) :: [Visual Studio Code] Kubernetes YAML 확장 팩 설치 및 YAML 언어 설정 (tistory.com)](https://rfriend.tistory.com/695)

- yaml extension 설치 
- 익스텐션 설정 
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FEQl0P%2FbtrhqK7mgZx%2F1JDAAMkj4iKmoQ2b3kjO90%2Fimg.png)
- setting.json에서 

```yml
{ 
	"yaml.schemas": 
		{ 
			"kubernetes": "*.yaml" 
		}, 
}  
```

## wavy yellow line 

- 위에 처럼 해도 없어지지 않는다! 

[One or more containers do not have resource limits - warning in VS Code Kubernetes tools - Stack Overflow](https://stackoverflow.com/questions/64080471/one-or-more-containers-do-not-have-resource-limits-warning-in-vs-code-kubernet)

setting -> json 수정 

```yaml
{
    "vs-kubernetes": {
        "disable-linters": ["resource-limits"],
        ...
    },
    ...
}
```