# Overview 

[4. Working with Environments · Pkg.jl (julialang.org)](https://pkgdocs.julialang.org/v1/environments/#Project-Precompilation)

- 줄리아 환경은  단순하게 운영된다. 
- 환경을 생성하고 싶은 디렉터리로 이동 
- 해당 디렉토리에서 Pkg 모드에서 `activate .`
- 해당 디레토리에 Project.toml, Manifest.toml 파일 두개가 생성된다. 
	- Manifest.toml 에는 필요한 패키지와 의존성 정보 
	- Project.toml에는 프로젝트 이름 
- Project.toml, Manifest.toml이 있다고 하자. 
	- 해당 디렉토리에서 Pkg 모드에서 `activate .`
	- `instantiate`를 실행하면 헤당 디렉토리에 패키지를 세팅한다. 

## Julia 버전 업 시 
```bash
$ activate . 
$ instantiate 
```
- 사이클을 반복해준다. 