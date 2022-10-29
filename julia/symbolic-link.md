# 심볼릭링크가 만들어지지 않을 때 

- 줄리아를 설치하고도 심볼릭 링크 만들어져  있지 않은 경우가 있다. 

## Macos 

```
sudo ln -s /Applications/Julia-x.x.x.app/Contents/Resources/julia/bin/julia /usr/bin/julia
```

```
sudo ln -s /Applications/Julia-x.x.x.app/Contents/Resources/julia/bin/julia /usr/local/bin/julia
```

