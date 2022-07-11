## Ubuntu 

- [Download Julia (julialang.org)](https://julialang.org/downloads/)
- 다운로드 디렉토리로 이동, 압축을 풀고, 심볼릭 링크를 생성한다. 
	- [How to Install Julia on Ubuntu | Ferrolho’s blog](https://ferrolho.github.io/blog/2019-01-26/how-to-install-julia-on-ubuntu)

```
cd ~/Downloads [다운로드 폴더/디렉토리를 의미]

# 파일 다운로드. wget을 이용하지 않고 직접 해도 된다. 
wget https://julialang-s3.julialang.org/bin/linux/x64/1.7/julia-1.7.2-linux-x86_64.tar.gz

# 압축 풀기 
tar -xvzf julia-1.7.2-linux-x86_64.tar.gz

# julia-1.7.2 디렉토리를 /opt 이하로 이동하기 
sudo cp -r julia-1.7.2 /opt/

# 심볼릭 링크 생성 
sudo ln -s /opt/julia-1.7.2/bin/julia /usr/local/bin/julia
```

## Macos 

#### M1
- Experimental을 깔았을 때 symlink 만들어주기 
```
sudo ln -s /Applications/Julia-1.8.app/Contents/Resources/julia/bin/julia 
/usr/local/bin/julia
```



## VS Code 

### WSL 2 
- WSL 2에 julialang, python 등을 설치했다고 가정하자. 
- Windows 에서 WSL2를 연결한 후 MS가 제공하는 각종 익스텐션을 인스톨하면 된다. 
	- Jupyter 
	- Python 
	- Julia 
