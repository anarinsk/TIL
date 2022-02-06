# pipreqs 

## Why 

- 프로젝트에서 활용하는 패키지 버전만 뽑아서 `requirements.txt`를 만든다. 

## 설치 

`!pip3 install pipreqs`

## 활용 

```shell
!pipreqs --force <Your-Local-DIR>
# Example
!pipreqs --force /home/jovyan/github-anari/project_stock-pandas/modules
```

- `<Your-Local-DIR>`은 프로젝트의 디렉토리를 나타낸다. 
- `.ipynb`은 해당 없음. `.py`를 분석해 import되는 패키지 버전을 파악하는 듯... 
- 파일을 읽고 import된 패키지와 버전을 `requirements.txt`로 해당 디렉토리에 생성한다. 
